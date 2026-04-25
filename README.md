<!-- NODE: REANS UENS | FRAME SYNC: LOCK | SIGNAL: NOMINAL -->

```
┌─────────────────────────── DOMAIN MAP ───────────────────────────┐
│                                                                   │
│   GNC / Sensor Fusion     Embedded / TinyML     Quantum / Cryo   │
│   ──────────────────       ──────────────        ───────────────  │
│   Kalman · Madgwick        Rust · STM32           BEC · Superfluid│
│   State-space · IMU        OV2640 · CNN INT8      4K nav · Phonon │
│                                                                   │
├─────────────────────── ACTIVE MISSIONS ──────────────────────────┤
│                                                                   │
│   [01] No-Drift Kalman Filter                                     │
│        28 trials · 62mm best · Target: IEEE Sensors              │
│        Δx̂ = K(z − Hx̂⁻)                                          │
│                                                                   │
│   [02] TinyML Edge Inference — STM32F407VET6                      │
│        OV2640 → DCMI → Cube.AI → GPIO latency probe             │
│                                                                   │
│   [03] BEC Atom Interferometry                                    │
│        Δφ = m·a·k_eff·T²/ℏ · Target: Acta Astronautica          │
│                                                                   │
│   [04] STRATUM — Research Registry Platform                       │
│        Axum · PostgreSQL · Cloudflare R2 · SvelteKit             │
│                                                                   │
├──────────────────────────── STACK ───────────────────────────────┤
│                                                                   │
│   Rust  ·  Python  ·  Julia  ·  Typst  ·  C  ·  SvelteKit       │
│   STM32F407  ·  ESP32-C3  ·  20MHz scope  ·  24MHz analyzer      │
│                                                                   │
│                                                                   │
│   DOMAIN  : GNC · Avionics · Embedded Systems                    │
│                                                                   │
└───────────────────────────────────────────────────────────────────┘
```

---

<div align="center">
<sub>uplink open · frame sync: lock · awaiting command vector</sub>
</div>
