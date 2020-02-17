# PathPlanner

[![Build Status](https://vikingrobotics.visualstudio.com/VIKING/_apis/build/status/FRC6854.PathPlannerViking?branchName=master)](https://vikingrobotics.visualstudio.com/VIKING/_build/latest?definitionId=2&branchName=master)

Inspiration came from [Vannaka's Generator](https://github.com/vannaka/Motion_Profile_Generator) which uses [Jaci's PathFinder](https://github.com/JacisNonsense/Pathfinder). The app is compatible with Windows, Mac OS, and Linux. It is also available on the Microsoft Store and Snapcraft Store.

## Working With Paths
<img align="right" width="400" src="https://i.imgur.com/mxX5ac0.png" alt="Point Configuration" />

Paths consist of two types of points: anchor and control points. Anchor points are points that *anchor* the path. They are points that the path will pass directly through. Control points are points that are attached to each anchor point. Control points can be used to fine-tune the curve of a path by pulling the path towards it. Anchor points, as well as their corresponding control points, can be added by right clicking anywhere on the field. They can be removed by by control/command + right clicking on the anchor point that you wish to remove. Any point on the path can be moved by dragging it around. While holding down the shift key and dragging a control point, its angle will be locked. You can right click on any anchor point to enter a position, change the angle (in degrees), and override the maximum velocity at that point. Overriding the velocity lets you slow down your robot at certain points in the path, which will prevent issues where the generation algorithm does not slow the robot down enough to accurately follow a tight curve, or it can just allow the robot to go slow in some areas (e.g. the area between the scale and switch) while maintaining a high speed during the rest of the path. When you are done editing the path, it can be saved and other paths can be loaded to edit. The path can then be generated for use on the robot or previewed in real time.

## Controls and Shortcuts
| Shortcut                                     | Description                              |
|----------------------------------------------|------------------------------------------|
| Left Click + Drag                            | Move Point                               |
| Right Click on Field                         | Add Point                                |
| Shift + Right Click on Field                 | Insert Point Between Two Other Points    |
| Right Click on Anchor Point                  | Edit Point Position/Angle/Velocity       |
| Ctrl/⌘ + Right Click on Anchor Point        | Delete Point                             |
| Shift + Click and Drag on Control Point      | Move Control Point with Angle Locked     |
| Shift + Click and Drag on Anchor Point       | Move Anchor point with Y Position Locked |
| Ctrl/⌘ + S                                  | Save Path                                |
| Ctrl/⌘ + O                                  | Open Path                                |
| Ctrl/⌘ + G                                  | Generate Path                            |
| Ctrl/⌘ + Shift + G                          | Generate Path with Last Used Settings    |
| Ctrl/⌘ + Shift + D                          | Deploy Generated Path to Robot           |
| Ctrl/⌘ + P                                  | Preview Path                             |
| Ctrl/⌘ + Z                                  | Undo                                     |
| Ctrl/⌘ + Y                                  | Redo                                     |
| Ctrl/⌘ + Shift + X                          | Flip path in the X direction             |
| Ctrl/⌘ + Shift + Y                          | Flip path in the Y direction             |

## Output Format Options
| Symbol | Description                                               |
|--------|-----------------------------------------------------------|
| x      | X Coordinate (Zeroed at start of path)                    |
| y      | Y Coordinate (Zeroed at start of path)                    |
| X      | Field Relative X Coordinate                               |
| Y      | Field Relative Y Coordinate                               |
| p      | Position (Center if single file, left/right if split)     |
| v      | Velocity (Center if single file, left/right if split)     |
| a      | Acceleration (Center if single file, left/right if split) |
| pl     | Left Only Position                                        |
| pr     | Right Only Position                                       |
| vl     | Left Only Velocity                                        |
| vr     | Right Only Velocity                                       |
| al     | Left Only Acceleration                                    |
| ar     | Right Only Acceleration                                   |
| h      | Absolute Heading in Degrees (-180 to 180)                 |
| H      | Relative Heading in Degrees (-180 to 180)                 |
| w      | Absolute Winding Heading in Degrees                       |
| W      | Relative Winding Heading in Degrees                       |
| t      | Time Elapsed                                              |
| s      | Time Step in Milliseconds                                 |
| S      | Time Step in Seconds                                      |
| r      | Curve Radius                                              |
| o      | Angular Velocity                                          |
| O      | Angular Acceleration                                      |

## Settings
<img align="right" width="400" src="https://i.imgur.com/PWDXw2K.png" alt="Robot Settings" />

* **Team Number:** Your team number. Used for uploading generated paths to the RoboRIO.
* **RoboRIO Path Location:** The folder on the RoboRIO that you would like the generated paths uploaded to.
* **Units:** The units to use for generation. (Imperial/Feet or Metric/Meters)
* **Game Year:** The game year to use for the field image.
* **Max Velocity:** Maximum velocity of the robot (units/second).
* **Max Acceleration:** Maximum acceleration of the robot (units/second<sup>2</sup>).
* **Coefficient of Friction:** The coeficcient of friction between the robot wheels and the floor. This is used to determine the max robot velocity in a curve. Andymark lists the coefficient of friction for most of their wheels on their website. Otherwise, you can try to calculate it yourself, or just tune this value until you find something that works.
* **Time Step:** The amount of time between each point in a profile in seconds.
* **Wheelbase Width:** The width of the robot's drive train, used for splitting the left and right paths.
* **Robot Length:** The length of the robot from bumper to bumper. This is used to draw the robot in the path preview and at the start/end points of the path.

## Path Generation
<img align="right" width="400" src="https://i.imgur.com/NGzXr75.png" alt="Path Generation" />

* **Output Type:** The output type. Options are CSV file, Java array, C++ array, or Python array. CSV files are saved to a chosen location and arrays are copied to the clipboard.
* **Path Name:** The name of the path. Underscores are assumed for CSV files and Python arrays while camel case is assumed for Java and C++ arrays
* **Output Format:** The format to use for the output of the generation. This should consist of one or more [output format options](#output-format-options) separated by commas.

    For example, a CSV file with format of p,v,a will output files where each line in the files is:

    `{position},{velocity},{acceleration}`
    
    **This field is case sensitive.**
* **Reversed Output:** Should the robot drive backwards
* **Split Path:** Should the generated path be split into two paths for each side of the drive train
* **Override End Velocity:** Should the path end with the velocity override of the last point instead of stopping

There are two different ways to generate paths. One is normal generation, where you can either save CSV files to your computer or arrays will be copied to your keyboard. The second option is deploying to the robot. This will generate CSV files and upload them to the RoboRIO (assuming you're connected to the robot) at the path chosen in the settings.

## How to build manually:
* Install [Node.js](https://nodejs.org)
* Clone this repository
* Run the following in the root directory of this project:
  * `npm install`
  
  * Build Windows: `npm run build-win`

  * Build MacOS: `npm run build-mac`

  * Build Linux: `npm run build-linux`
  
  * Run in Development Mode: `npm start`
* The built application will be located in `/dist`
