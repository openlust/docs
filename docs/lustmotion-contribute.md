# Contribute

## Contribute a Pattern

Making your own pattern is not that hard. They can be found in the header only [pattern.h](./src/pattern.h) and easily extended.

### Subclass Pattern in pattern.h

To create a new pattern just subclass from `class Pattern`. Have a look at `class SimpleStroke` for the most basic implementation:

```cpp
class SimpleStroke : public Pattern {
    public:
        SimpleStroke(const char *str) : Pattern(str) {}
```

Add the constructor to store the patterns name string.

Reimplement set-functions if you need them to do some math:

```cpp
        void setTimeOfStroke(float speed = 0) {
             // In & Out have same time, so we need to divide by 2
            _timeOfStroke = 0.5 * speed;
        }
```

Reimplement the core function `motionParameter nextTarget(unsigned int index)`. This is mandatory, as the StrokeEngine will call this function after each stroke to get the next set of `motionParameter`. Each time this function is called the `index` increments by 1. If the pattern is called the very first time this always starts as 0. This can be used to create pattern that vary over time:

```cpp
        motionParameter nextTarget(unsigned int index) {
            // maximum speed of the trapezoidal motion
            _nextMove.speed = int(1.5 * _stroke/_timeOfStroke);

            // acceleration to meet the profile
            _nextMove.acceleration = int(3.0 * _nextMove.speed/_timeOfStroke);

            // odd stroke is moving out
            if (index % 2) {
                _nextMove.stroke = 0;

            // even stroke is moving in
            } else {
                _nextMove.stroke = _stroke;
            }

            _index = index;
            return _nextMove;
        }
};
```

If you need further helper functions and variables use the `protected:` section to implement them.

Don't forget to add an instance of your new pattern class at the very bottom of the file to the `*patternTable[]`-Array.

```cpp
static Pattern *patternTable[] = {
  new SimpleStroke("Simple Stroke"),
  new TeasingPounding("Teasing or Pounding")
  // <-- insert your new pattern class here!
 };
```

#### Pauses

It is possible for a pattern to insert pauses between strokes. The main stroking-thread of StrokeEngine will poll a new set of motion commands every few milliseconds once the target position of the last stroke is reached. If a pattern returns the motion parameter `_nextMove.skip = true;` inside the costume implementation of the `nextTarget()`-function no new motion is started. Instead it is polled again later. This allows to compare `millis()` inside a pattern. To make this more convenient the `Pattern` base class implements 3 private functions: `void _startDelay()`, `void _updateDelay(int delayInMillis)` and `bool _isStillDelayed()`. `_startDelay()` will start the delay and `_updateDelay(int delayInMillis)` will set the desired pause in milliseconds. `_updateDelay()` can be updated any time with a new value. If a stroke becomes overdue it is executed immediately. `bool _isStillDelayed()` is just a wrapper for comparing the current time with the scheduled time. Can be used inside the `nextTarget()`-function to indicate whether StrokeEngine should be advised to skip this step by returning `_nextMove.skip = true;`. See the pattern Stop'n'Go for an example on how to use this mechanism.

### Expected Behavior

#### Adhere to Depth & Stroke at All Times

Depth and Stroke set in StrokeEngine are axiomatic. StrokeEngine closely monitors the returned `motionParameter` and ensures no violation against the machines physics were returned. Pattern only return a stroke information which is offset by depth in the StrokeEngine. Your return value may be anywhere in the interval [0, stroke]. Positions outside the interval [depth - stroke, depth] will be truncated, leading to a distortion of your intended stroke profile. This is an integral safety feature to prevent injuries. This sets the envelope the pattern may use. Similar for speed a.k.a. timeOfStroke.

#### Use `index` Properly

`index` provides further information then just the stroke count:

- It always starts at `0` if a pattern is called the first time. It resets with every call of `StrokeEngine.setPattern(int)` or `StrokeEngine.startMotion()`.
- It increments after each successfully executed move.
- Store the last index in `_index` before returning. By comparing `index == _index` you can determine that this time it is not a new stroke, but rather an update of a current stroke. This information can be handy in pattern varying over time.
