# Safe Usage

## Main Controls

### Depth

### Stroke

### Speed

### Sensation

### Speed Preference

### Fixed Positions

## Pattern

Patterns are what set LUST-motion apart. They allow to bring a lot of variety into play. Pattern are small programs that StrokeEngine is using to create the next set of trapezoidal motion parameter (Target Position, Speed & Acceleration).

### Teasing or Pounding

The sensation value can change the speed ratio between in and out. Sensation > 0 makes the in-move faster (up to 5x) giving a hard pounding sensation. Values < 0 make the out-move going faster. This gives a more pleasing sensation. The time for the overall stroke remains always the same and only depends on the global speed parameter.

### Robo Stroke

Sensation controls the acceleration of the stroke. Positive value increase acceleration until it is a constant speed motion (feels robotic). Neutral is equal to simple stroke (1/3, 1/3, 1/3). Negative reduces acceleration into a triangle profile.

### Half'n'Half

Similar to Teasing or Pounding, but every second stroke is only half the depth. The sensation value can change the speed ratio between in and out. Sensation > 0 make the in move faster (up to 5x) giving a hard pounding sensation. Values < 0 make the out move going faster. This gives a more pleasing sensation. The time for the overall stroke remains the same for all strokes, even half ones.

### Deeper

The insertion depth ramps up gradually with each stroke until it reaches its maximum. It then resets and restarts. Sensations controls how many strokes there are in a ramp.

### Stop'n'Go

Pauses between a series of strokes. The number of strokes ramps from 1 stroke to 5 strokes and back. Sensation changes the length of the pauses between stroke series.

### Insist

Sensation reduces the effective stroke length while keeping the stroke speed constant to the full stroke. This creates interesting vibrational pattern at higher sensation values. With positive sensation the strokes will wander towards the front, with negative values towards the back.

### Random Depth

The depth of the stroke is random. The velocity is kept constant, so that shorter stroke will have a higher than nominal rate. Sensation changes the ration between in- and out-speed.

## Safety Settings

### Range Limit

### Velocity Limit

### Heartbeat Mode
