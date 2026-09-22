# Formula Student AI — portfolio

Public write-up of my work as **Software Lead** with **UHRA** (University of Hertfordshire Racing Autonomous) on Formula Student AI — planning and control for a driverless car.

**Team:** [uhracingautonomous.netlify.app/team](https://uhracingautonomous.netlify.app/team)  
**Live site:** [sanchitacharya.github.io/FS-AI-Portfolio](https://sanchitacharya.github.io/FS-AI-Portfolio/)  

**This repository does not contain team source code.**

---

## How the pipeline fits together

At a high level the car runs a classic autonomy loop. Nothing proprietary here — just the shape of the system:

1. **See the world** — sensors (camera, and later lidar) build a picture of cones and the track.
2. **Know where you are** — localization turns that into a pose (where the car is and which way it’s pointing).
3. **Decide where to go** — planning builds a safe path for the current mission (straight corridor, figure-eight, lap, …).
4. **Drive it** — control turns that path into steering and speed commands the vehicle can follow.
5. **Finish cleanly** — when the mission ends, stop in the right place and hand off to the finished state.

Simulation is used to iterate quickly; the real car is the only test that counts. Gaps between sim and track (cone spacing, stop zones, how hard the car reacts) are where most of the hard lessons lived.

```text
  sensors  →  localization  →  planning  →  control  →  vehicle
                 ↑                              |
                 └──────── feedback (pose / speed) ────┘
```

My focus sat mainly in **planning and control** for acceleration and skidpad, with a clear next step to strengthen **sensing and localization** so those missions (and the rest) hold up when the cones don’t match the sim.

---

## What’s on the site

### Competition
The four dynamic missions: **Acceleration**, **Skidpad**, **Autocross / Sprint** (one timed lap), and **Trackdrive** (multi-lap endurance).

### Acceleration
Drift builds up on a “straight” run; over-correcting at speed makes the car wobble. Goal: stay in the corridor, correct gently, finish the stop. Sim was updated after real-car runs (stop zones differ). UHRA’s **first acceleration point** — completed, if not fast. Footage: sim + real.

### Skidpad
Right circle ×2 → left circle ×2 → straight out into the orange finish zone. Built in ~6 hours to probe sim vs real without lidar / full localization. Concept in sim; real cone layout diverged, so the track wasn’t completed on the day.

### Roadmap
Bring **lidar + IMU** into localization, then harden acceleration and skidpad and push **Autocross / Sprint** and **Trackdrive** on the same solid pose.

---

Open the live link for the full page (layout, videos, detail). This README is the short public version only.
