# Aram
Aram is an open-source framework for simulating classical physics systems using numerical methods. It provides modular components for mechanics, fields, and differential equations, designed to run efficiently on standard hardware.

---

## Vision

- Make physics simulations transparent, interactive, and educational  
- Provide modular tools for mechanics, fields, and differential equations  
- Run efficiently on standard consumer hardware  
- Serve as a learning platform for numerical methods, system design, and visualisation

---

## Architecture

| Layer      | Responsibility                               |
|------------|----------------------------------------------|
| Model      | Physics equations only                        |
| Solver     | Numerical methods (Euler, RK4, etc.)        |
| System     | State + time evolution                        |
| Experiment | Initial conditions + parameters              |
| Output     | CSV, plots, analysis                          |

**Design principle:** solver abstractions decouple computation from loops, enabling future GPU acceleration.

---

## Detailed MVP Roadmap

### **MVP 1 — Sandbox & Single Particle (Foundation)**

**Goal:** One complete simulation with interactive sandbox UI  

**Physics Covered:**
- 1D Motion: Free fall, constant velocity, harmonic oscillator (`x'' + (k/m)x = 0`)  

**Forces / Effects:** Gravity, air resistance  

**UI / Sandbox Features:**
- Drag-and-drop particle to set initial position  
- Input mass, initial velocity, gravity, air resistance  
- Start / Pause / Reset simulation  
- Real-time x(t) plot  
- Optional CSV download  

**Solver:** Euler & RK4  

---

### **MVP 2 — Reusable Simulation Engine**

**Goal:** Make Aram a modular simulation framework  

**Physics Covered:**
- 2D Motion: Projectile motion, damped harmonic oscillator  

**Forces / Effects:** Gravity (2D), air resistance, linear spring forces  

**Features:**
- `PhysicalModel` & `ODESolver` interfaces  
- Config-driven experiments  
- Multiple runs with parameter variations  
- CSV + plots  

**Visualization:** 2D trajectories, x(t) and y(t) plots  

---

### **MVP 3 — Desmos-Like Core & User-Defined Equations**

**Goal:** Allow arbitrary user-defined equations  

**Physics Covered:**
- General ODEs: damped driven oscillators, coupled systems, simple pendulum  
- User-defined forces  

**Features:**
- Equation parser (string → function)  
- Phase-space plotting (x vs vx)  
- Parameter sweeps (CPU-parallel, GPU-ready)  

**Visualization:** x(t), y(t) plots; phase-space plots; multiple runs comparison  

---

### **MVP 4 — Full Graphical Sandbox / Multi-Particle Physics**

**Goal:** Interactive sandbox with multiple particles  

**Physics Covered:**
- Multi-particle interactions: collisions (elastic & inelastic), center-of-mass, N-body gravity  

**Forces / Effects:** Gravity, air resistance, spring forces, user-defined forces  

**UI / Sandbox Features:**
- Drag-and-drop positions for multiple particles  
- Input mass, velocities, forces  
- Force toggles: gravity, air, springs, user-defined  
- Start / Pause / Reset simulation  
- Real-time plots: positions, velocities, energies  

**Visualisation:** 2D particle animation, phase-space plots, trajectory trails  

---

### **MVP 5 — GPU / Large-Scale Physics (Optional / Advanced)**

**Goal:** Enable GPU-accelerated simulations for large particle counts  

**Physics Covered:**
- Large N-body gravitational systems  
- Particle systems: collisions, drag, springs  
- Monte Carlo experiments for chaotic systems  

**Features:**
- OpenCL / CUDA or Python GPU kernels  
- Stateless, immutable solver architecture  
- Parallel computation for parameter sweeps  
- High-resolution trajectory plots  

**Visualization:** 2D / optional 3D rendering, trajectory heatmaps  

---

### Optional / Future Physics Extensions
- Pendulum arrays  
- Coupled oscillators  
- Chaotic systems (double pendulum, Lorenz attractor)  
- Projectile motion with quadratic drag  

---

## GPU Strategy (Future-Proof)

- **Phase 1:** CPU-first, GPU-ready (stateless solvers, immutable state)  
- **Phase 2:** Parallel CPU (ForkJoinPool for parameter sweeps)  
- **Phase 3:** GPU via OpenCL/CUDA/Python bridge only when needed  

**Design rule:** Solver ≠ Loop  
- Bad: `for(t...) { update(); }`  
- Good: `solver.integrate(model, state, timeGrid);`  

---

## How to Contribute

1. Fork the repository  
2. Create a feature branch:  
```bash
git checkout -b feature/mvp1-sandbox
