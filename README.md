<!-- ============================================================ -->
<!--  NODE IDENTITY: Reans Uens                                  -->
<!--  CALLSIGN: reans-uens                                       -->
<!--  LINK LAYER: GitHub Profile README                          -->
<!--  CLASSIFICATION: PUBLIC / OPEN CHANNEL                      -->
<!--  FRAME SYNC: ESTABLISHED                                    -->
<!-- ============================================================ -->

<div align="center">

```
╔══════════════════════════════════════════════════════════════════╗
║  UPLINK ESTABLISHED — NODE: REANS UENS                          ║
║  FRAME SYNC: LOCK      CARRIER: STABLE      SNR: NOMINAL        ║
║  SUBSYSTEM: GNC / AVIONICS / EMBEDDED / QUANTUM                 ║
╚══════════════════════════════════════════════════════════════════╝
```

</div>

---

## `OPERATOR_PROFILE :: REANS_UENS`

```ada
-- ENTITY DECLARATION
-- Source: University of Baghdad, Aeronautical Engineering, Year 5
-- Specialization Track: GNC | Avionics | Embedded Systems
-- Clearance Vector: Research / Grad-School Candidate
-- Target Nodes: TU Delft | KTH | Imperial College London

procedure INIT_OPERATOR (
   Name         : constant String  := "Reans Uens";
   Domain       : constant String  := "Guidance, Navigation & Control";
   Stack        : constant String  := "Rust / Python / Julia / Typst / C";
   Clearance    : constant Integer := 5;  -- Fifth-year standing
   Status       : constant String  := "ACTIVE — SEEKING POSTGRADUATE LINK"
) is begin
   HANDSHAKE_COMPLETE;
end INIT_OPERATOR;
```

---

## `SUBSYSTEM_MAP :: TECHNICAL_DOMAINS`

```
┌─────────────────────────────────────────────────────────────────────────┐
│  DOMAIN TREE — ACTIVE NODES                                             │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  GNC_CORE ──────────────── Kalman Filter (no-drift variant)            │
│       │                    Complementary / Madgwick Fusion              │
│       │                    State-Space Formulation                      │
│       │                    Lateral Derivatives, Phugoid Modes           │
│       └── SENSOR_FUSION ── IMU | Magnetometer | Odometry               │
│                            Bare-metal Rust on ESP32-C3 / STM32         │
│                                                                         │
│  EMBEDDED ─────────────── No-OS bare-metal firmware (Rust)             │
│       │                   DCMI camera interface (OV2640)                │
│       │                   GPIO latency instrumentation                  │
│       └── INFERENCE ────── TinyML / STM32Cube.AI                       │
│                            Quantized CNN, edge deployment               │
│                            STM32F407 target platform                    │
│                                                                         │
│  QUANTUM_SYSTEMS ──────── BEC atom interferometry                      │
│       │                   Inertial navigation via quantum phase shift    │
│       │                   Superfluid Bose liquid thermodynamics         │
│       └── CRYO ─────────── 4K aerospace systems                        │
│                            Superconductor manufacturing                  │
│                            Heat transfer: phonon / roton modes          │
│                                                                         │
│  PROPULSION ───────────── Ramjet | Turbojet | Turbofan | Turboprop     │
│       │                   Cycle analysis, Julia thermodynamic sim       │
│       └── STRUCTURES ───── Multicell wing shear flow                   │
│                            Fatigue: Soderberg | von Mises               │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## `ACTIVE_MISSION_REGISTRY`

### `[MISSION_01] :: TinyML Edge Inference — STM32F407`

```rust
// TARGET PLATFORM: STM32F407VET6
// INFERENCE ENGINE: STM32Cube.AI (quantized CNN)
// SENSOR BUS: OV2640 via DCMI
// LATENCY PROBE: GPIO toggle method

fn mission_gnc_tinyml() -> MissionStatus {
    let camera   = DCMI::init(OV2640_CONFIG);
    let model    = CubeAI::load(QUANTIZED_CNN);
    let t_start  = GPIO::timestamp();
    let result   = model.infer(&camera.capture());
    let latency  = GPIO::timestamp() - t_start;
    MissionStatus::Active { latency_us: latency }
}
```

**Key parameters:**
- Inference latency target: `< T_frame / 2`
- Quantization: INT8 post-training
- Output: object classification vector `y ∈ ℝⁿ`

---

### `[MISSION_02] :: No-Drift Kalman Filter — Heading Estimation`

State vector: `x = [θ, ω, b]ᵀ` (heading, angular rate, gyro bias)

```
Predict:   x̂⁻ = F·x̂ + B·u
           P⁻  = F·P·Fᵀ + Q

Update:    K   = P⁻·Hᵀ·(H·P⁻·Hᵀ + R)⁻¹
           x̂   = x̂⁻ + K·(z − H·x̂⁻)
           P   = (I − K·H)·P⁻
```

**Experimental result:** 28-trial differential-drive robot, 800mm square trajectory.
Best heading error: `~62mm` (Madgwick variant). Target publication: *IEEE Sensors*.

---

### `[MISSION_03] :: BEC Atom Interferometry — Inertial Navigation`

Phase shift due to inertial acceleration `a`:

```
Δφ = (m · a · k_eff · T²) / ℏ
```

Where:
- `m`       = atomic mass (Rb-87)
- `k_eff`   = 2·k_laser (two-photon recoil)
- `T`       = free-evolution time
- `ℏ`       = reduced Planck constant

Sensitivity bound (shot-noise limited):

```
δa_min = 1 / (k_eff · T² · √N)    [m/s² / √Hz]
```

Target publication: *Acta Astronautica*.

---

### `[MISSION_04] :: STRATUM — Undergraduate Research Registry`

```
ARCHITECTURE STACK:
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│  SvelteKit   │────▶│ Axum/FastAPI │────▶│  PostgreSQL  │
│  (Frontend)  │     │  (Backend)   │     │  (Storage)   │
└──────────────┘     └──────────────┘     └──────────────┘
                             │
                      ┌──────▼──────┐
                      │ Cloudflare  │
                      │     R2      │
                      └─────────────┘
PHASE: ACTIVE BUILD
PURPOSE: Undergraduate research visibility infrastructure
```

---

## `HARDWARE_MANIFEST`

```
PROCESSOR   : Intel Core i9-13900H
GPU         : NVIDIA RTX 3050 (Mobile Thin)
RAM         : 16 GB DDR5
MCU         : STM32F103C8T6 (active lab unit)
SCOPE       : 20 MHz oscilloscope
ANALYZER    : 24 MHz logic analyzer
TARGET_MCU  : STM32F407VET6 (graduation project)
```

---

## `LANGUAGE_AND_TOOLCHAIN_MATRIX`

| Language | Domain | Proficiency |
|----------|--------|-------------|
| `Rust` | Bare-metal embedded, systems | PRIMARY |
| `Python` | ML pipelines, scripting | OPERATIONAL |
| `Julia` | Thermodynamic simulation, numerical | OPERATIONAL |
| `Typst` | Technical documentation | OPERATIONAL |
| `C` | STM32 HAL, CMSIS | FUNCTIONAL |
| `Ada` | Formal spec reference | STUDY |
| `JavaScript/Svelte` | Web frontend (STRATUM) | FUNCTIONAL |

---

## `PUBLICATION_PIPELINE`

```
┌─────────────────────────────────────────────────────┐
│  PAPER_01: No-Drift Kalman Filter                   │
│  Target  : IEEE Sensors                             │
│  Status  : TRIALS COMPLETE — STATS EXPANSION REQ'D │
│  Data    : 28 trials, 4 filter variants             │
├─────────────────────────────────────────────────────┤
│  PAPER_02: BEC Atom Interferometry                  │
│  Target  : Acta Astronautica                        │
│  Status  : MATH PIPELINE UNDER DEVELOPMENT          │
│  Scope   : Quantum inertial nav for aerospace       │
└─────────────────────────────────────────────────────┘
```

---

## `LONG_RANGE_NAVIGATION_PLAN`

```
CURRENT_POSITION : Baghdad, Iraq — Year 5 Aeronautical Engineering
WAYPOINT_ALPHA   : Graduate thesis delivery — STM32 TinyML
WAYPOINT_BETA    : Dual publication (IEEE + Acta Astronautica)
WAYPOINT_GAMMA   : MSc application transmission
TARGET_NODES     : TU Delft | KTH Stockholm | Imperial College London
SPECIALIZATION   : GNC | Avionics | Embedded Systems
ETA              : 2025–2026 enrollment window
```

---

## `RESEARCH_INTEREST_SPECTRUM`

```
FREQUENCY DOMAIN (ranked by signal strength):

  Quantum Inertial Navigation ████████████████████ MAX
  BEC / Superfluid Dynamics   ██████████████████░░
  Sensor Fusion (KF/Madgwick) █████████████████░░░
  TinyML on Microcontrollers  ████████████████░░░░
  Cryogenic Heat Transfer     ██████████████░░░░░░
  GNC Algorithms              ████████████████████ MAX
  Embedded Rust (no-OS)       █████████████████░░░
  Flight Dynamics             ██████████████░░░░░░
  Propulsion Thermodynamics   ████████████░░░░░░░░
```

---

## `CONTACT_VECTOR`

```
NODE     : Reans Uens
PLATFORM : GitHub
CHANNEL  : Open
AFFIL    : University of Baghdad, Aeronautical Engineering
MISSION  : Postgraduate research, GNC/Avionics/Quantum systems
```

---

<div align="center">

```
╔══════════════════════════════════════════════════════════════════╗
║  FRAME_CLOSE :: ALL SUBSYSTEMS NOMINAL                          ║
║  CHECKSUM: VERIFIED   SIGNAL: STABLE   NODE: SYNCHRONIZED       ║
║  AWAITING NEXT COMMAND VECTOR...                                 ║
╚══════════════════════════════════════════════════════════════════╝
```

</div>
