**Status: Reflects implementation as of v0.2.19**

# Work Breakdown Structure & Roadmap

## Current State (v0.2.19)

### Completed Features

| Feature | Version | Status |
|---------|---------|--------|
| Snapclient audio playback | v0.1.0 | ✅ Stable |
| Album art + metadata display | v0.1.0 | ✅ Stable |
| Real-time spectrum analyzer | v0.1.0 | ✅ Stable |
| 15 audio HAT support + auto-detection | v0.2.0+ | ✅ Stable |
| Zero-touch SD install | v0.1.0 | ✅ Stable |
| Read-only filesystem (overlayfs) | v0.1.3 | ✅ Stable |
| Song progress bar with local clock interpolation | v0.1.8 | ✅ Stable |
| Source label + format badge | v0.1.8 | ✅ Stable |
| Non-root containers with minimal capabilities | v0.1.7 | ✅ Stable |
| Centralized metadata service integration | v0.2.0 | ✅ Stable |
| Big-endian support (PowerPC) | v0.2.1 | ✅ Stable |
| mDNS server discovery on boot | v0.2.1 | ✅ Stable |
| Unified SNAPSERVER_HOST configuration | v0.2.1 | ✅ Stable |
| ALSA & network auto-tuning | v0.2.2 | ✅ Stable |
| WiFi power-save disable | v0.2.2 | ✅ Stable |
| App version in status line | v0.2.3 | ✅ Stable |
| Server version in status line | v0.2.4 | ✅ Stable |
| I2C HAT detection (EEPROM-less boards) | v0.2.6+ | ✅ Stable |
| Display profile auto-detection at boot | v0.2.10+ | ✅ Stable |

### Architecture Decisions Made

| Decision | Rationale | Status |
|----------|-----------|--------|
| Centralized metadata service | Eliminate N clients making N API calls | ✅ Implemented |
| Direct framebuffer rendering | No X11/Wayland overhead | ✅ Implemented |
| ALSA loopback for spectrum | Zero-latency audio capture | ✅ Implemented |
| Docker Compose profiles | Headless vs display mode | ✅ Implemented |
| Resource limit auto-detection | Pi model-specific tuning | ✅ Implemented |
| Read-only root filesystem | SD card protection | ✅ Implemented |

## Known Issues & Limitations

| Issue | Impact | Status |
|-------|--------|--------|
| Python tests not in CI | Coverage gap | ⚠️ To be addressed |
| Pi 5 compatibility unverified | Hardware support gap | ⚠️ Testing needed |
| No OTA update mechanism | Manual updates required | 📋 Future work |

## Roadmap

### Next Priority: CI Integration

| Task | Description | Complexity |
|------|-------------|-----------|
| Add pytest to CI | Include Python unit tests in GitHub Actions | Low |
| Fix test dependencies | Ensure numpy/pillow available in CI | Low |
| Coverage reporting | Add coverage metrics to PR comments | Medium |

### Future: Multi-Display Layout Templates

Aspect-ratio-specific layout templates to optimize the display for different screen geometries.

| Task | Description | Complexity |
|------|-------------|-----------|
| Define layout profiles | Map aspect ratios (16:9, 4:3, ~16:10) to layout parameters | Medium |
| Auto-detect aspect ratio | Compute ratio from framebuffer dimensions, select best template | Low |
| 4:3 template | Optimize for 1024x768 (iBook, old monitors) — taller spectrum, smaller art | Medium |
| 16:10 template | Optimize for 1024x600 (common touchscreens) | Medium |
| Portrait mode | Vertical layout for rotated displays | High |

### Potential Future Work

| Area | Description | Priority |
|------|-------------|----------|
| Pi 5 validation | Test on Pi 5 hardware, update compatibility matrix | Medium |
| Pi Zero 2 W audio-only | Headless mode without display containers | Low |
| OTA updates | Pull new images and restart without SSH | Low |
| Touch controls | Volume/transport via touchscreen (basic framework exists) | Low |
| Multi-language | Localized setup script prompts | Very Low |

## Quality Metrics

| Metric | Current | Target |
|--------|---------|--------|
| Unit tests (pytest) | 109 (82 display + 27 visualizer) | 120+ |
| Shell tests | 37 (15 HAT + 22 entrypoint) | 40+ |
| HAT configs validated | 15/15 | 15/15 |
| Shell scripts passing shellcheck | All | All |
| CI pipeline | lint + shell tests + review | + Python tests |
| Supported platforms | ARM64 + PowerPC | + Pi 5 verification |
| Documentation | Planning docs updated to v0.2.19 | Keep current |

## Development Process Maturity

✅ **Achieved**:
- Pre-push hooks with local CI
- Automated Docker builds on tag
- Code review automation
- Comprehensive test suite (unit + integration)
- Security hardening (containers + filesystem)
- Zero-touch deployment

📋 **Next Level**:
- Python tests in CI pipeline
- Performance benchmarks
- Hardware-in-the-loop testing