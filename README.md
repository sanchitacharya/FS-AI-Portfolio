# Formula Student AI — portfolio

Public write-up of my UHRA Formula Student AI work (planning & control).  
**This repo does not contain team source code.**

---

## What is Formula Student AI?

Formula Student driverless challenges university teams to build a small race car that can drive itself. Software has to perceive the track, plan a path, and send steering and acceleration commands — in simulation first, then on a real vehicle.

Missions are short, scored events. Formula Student AI has four main dynamic ones:

| Mission | What it is |
| --- | --- |
| **Acceleration** | Leave the line, stay in a cone corridor, stop cleanly at the end. |
| **Skidpad** | Two right circles, two left circles, then exit straight and stop in the orange finish zone. |
| **Autocross / Sprint** | One timed lap of a handling track (corners, chicanes, hairpins). Go once, stop, done. No reusing map data from a previous run. |
| **Trackdrive** | About ten laps of a closed cone circuit — endurance / reliability, not a single hot lap. Biggest points event. |

---

## Acceleration planning & control

**UHRA · first acceleration point**

Acceleration looks simple — mostly a straight shot — but it isn’t. Small drift builds up over the corridor, and at speed it’s hard to keep the car steady without over-steering and starting to wobble.

The job was to keep the car in the cone corridor, correct gently when it drifted, and still stop cleanly at the end so the mission could finish.

After we saw the real car, we updated the simulation to better match how it actually behaved — including less harsh steering. The sim clip can look like it goes past the orange cone; that is partly because the stopping zone in simulation is smaller than in real life.

On the real track, UHRA scored its first ever acceleration point and completed the run. It was not a fast time — but we finished the corridor and got the result on the board.

- Problem: lateral drift accumulates; over-correcting at speed makes the car unstable.
- Goal: stay centred in the corridor and finish the stop without fighting the wheel.
- Process: tune after real-car runs, then bring those lessons back into simulation.
- Sim vs reality: smaller stop zone in sim can show past the orange cone; real finish area is larger.
- Result: UHRA’s first acceleration point — completed, if not quick.

**Simulation (after real-car lessons)**

<video src="videos/acceleration-sim.mp4" controls width="720"></video>

**Real life (first UHRA point)**

<video src="videos/acceleration-real.mp4" controls width="720"></video>

---

## Skidpad attempt

**Built in ~6 hours · incomplete on the real car**

Official skidpad is a figure-eight: enter the course, complete two laps of the right circle, then two laps of the left circle, then exit straight through the intersection and stop in the marked orange finish / exit zone.

This version was put together in about six hours so we could compare simulation against the real car. We did not have lidar in the loop, and localization was not ready yet — so the run had to lean on simpler, opportunistic ways to get around the figure-eight and try to finish.

The concept was there, and the sim run shows the idea. On the real car it did not hold together: cone layout and spacing did not match what we had in simulation, so the last pieces of finish logic were never brought in. We did not complete the track on the day — but the rush build still showed where sim and reality diverge.

- Mission: right circle ×2 → left circle ×2 → straight out → stop in the orange zone.
- Constraint: ~6-hour build to probe sim vs real, without lidar / full localization.
- Blocker: real cone positions differed from the sim world; final finish logic was not introduced.
- Outcome: concept demonstrated in simulation; track not completed on the real car.

**Skidpad simulation**

<video src="videos/skidpad-sim.mp4" controls width="720"></video>

---

## What’s next

**Software lead · UHRA**

This year I am the software lead. The gap from last season is clear: without solid sensing and localization, clever mission hacks only go so far — especially once cone layouts leave the simulator.

Next steps are to bring lidar into the loop and build localization from lidar + IMU. I am looking at HKU’s Fast-LIO as a starting point for that odometry / mapping layer, then using a better pose estimate to harden every mission.

On the mission side: keep improving acceleration and skidpad, and push Autocross / Sprint plus Trackdrive so the stack can do a single hot lap and a long multi-lap run — not just the straight corridor.

- Role: software lead for UHRA this season.
- Sensing: use lidar (with IMU) instead of running blind on weak localization.
- Localization: explore HKU Fast-LIO and fit it to the car’s stack.
- Missions: optimize acceleration, skidpad, Autocross / Sprint, and Trackdrive.

---

## Stack (high level)

Work sat in a ROS 2 autonomy stack: trajectories in, steer + accel commands out, with simulation for iteration and a real vehicle for the final test.

`ROS 2 Humble` · `Planning & control` · `Steer + accel commands` · `Odometry / EKF` · `Gazebo` · `Docker`
