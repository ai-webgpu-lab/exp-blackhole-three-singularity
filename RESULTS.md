# Results

## 1. 실험 요약
- 저장소: exp-blackhole-three-singularity
- 커밋 해시: 7d6a2d6
- 실험 일시: 2026-05-20T15:40:41.347Z -> 2026-05-20T15:40:47.703Z
- 담당자: ai-webgpu-lab
- 실험 유형: `blackhole`
- 상태: `success`

## 2. 질문
- three.js/TSL 블랙홀 실험으로 넘기기 전에 lensing scene load와 frame pacing 보고 경로를 먼저 고정할 수 있는가
- ray step budget, TAA state, adaptive quality metadata가 graphics 결과 문서에 같이 남는가
- 실제 WebGPU/WebGL renderer 교체 전 deterministic blackhole harness로 반복 검증이 가능한가

## 3. 실행 환경
### 브라우저
- 이름: Chrome
- 버전: 147.0.7727.15

### 운영체제
- OS: Linux
- 버전: unknown

### 디바이스
- 장치명: Linux x86_64
- device class: `desktop-high`
- CPU: 16 threads
- 메모리: 32 GB
- 전원 상태: `unknown`

### GPU / 실행 모드
- adapter: navigator.gpu available
- backend: `webgpu`
- fallback triggered: `false`
- worker mode: `main`
- cache state: `warm`
- required features: ["shader-f16","timestamp-query"]
- limits snapshot: {"maxTextureDimension2D":8192,"maxBindGroups":4}

## 4. 워크로드 정의
- 시나리오 이름: Blackhole Singularity Readiness, blackhole-three-singularity-real-blackhole-three-01600
- 입력 프로필: single-kerr-style-lensing-fixture
- 데이터 크기: raySteps=96; diskSamples=144; photonRingSamples=72; backend=webgpu; fallback=false; automation=playwright-chromium, raySteps=96; diskSamples=144; photonRingSamples=72; backend=webgpu; fallback=false; realAdapter=blackhole-three-01600; automation=playwright-chromium
- dataset: -
- model_id 또는 renderer: three-tsl-webgpu-readiness
- 양자화/정밀도: -
- resolution: 960x540
- context_tokens: -
- output_tokens: -

## 5. 측정 지표
### 공통
- time_to_interactive_ms: 728.4 ~ 1639.5 ms
- init_ms: 4.4 ~ 36.2 ms
- success_rate: 1
- peak_memory_note: 32 GB reported by browser
- error_type: -

### Graphics / Blackhole
- avg_fps: 58.98 ~ 4324.32
- p95_frametime_ms: 0.3 ~ 18 ms
- scene_load_ms: 4.4 ~ 36.2 ms
- ray_steps: 96
- taa states: true
- fallback states: false
- backends: webgpu

## 6. 결과 표
| Run | Scenario | Backend | Cache | Mean | P95 | Notes |
|---|---|---:|---:|---:|---:|---|
| 1 | Blackhole Singularity Readiness | webgpu | warm | 58.98 | 18 | scene_load=36.2 ms, fallback=false |
| 2 | blackhole-three-singularity-real-blackhole-three-01600 | webgpu | warm | 4324.32 | 0.3 | scene_load=4.4 ms, fallback=false |

## 7. 관찰
- blackhole singularity baseline은 backend=webgpu, fallback_triggered=false로 기록됐다.
- graphics summary는 avg_fps=58.98, p95_frametime_ms=18, scene_load_ms=36.2였다.
- lensing metadata는 ray_steps=96, taa_enabled=true, resolution_scale=0.82로 남았다.
- playwright-chromium로 수집된 automation baseline이며 headless=true, browser=Chromium 147.0.7727.15.
- 실제 runtime/model/renderer 교체 전 deterministic harness 결과이므로, 절대 성능보다 보고 경로와 재현성 확인에 우선 의미가 있다.

## 8. Real Adapter vs Deterministic
- adapter: real=blackhole-three-01600, deterministic=deterministic-three-style
- avg_fps: real=4324.32, deterministic=58.98, delta=+4265.34
- p95_frametime: real=0.3 ms, deterministic=18 ms, delta=-17.7 ms
- scene_load_ms: real=4.4 ms, deterministic=36.2 ms, delta=-31.8 ms

## 9. 결론
- three.js/TSL 블랙홀 실험으로 넘어가기 전 lensing scene readiness baseline과 결과 문서가 연결됐다.
- 다음 단계는 deterministic canvas surface를 실제 three.js WebGPU/WebGL renderer로 교체하되 ray_steps, TAA, frame pacing metric 구조를 유지하는 것이다.
- 이후 blackhole renderer shootout의 첫 입력 baseline으로 재사용할 수 있다.

## 10. 첨부
- 스크린샷: ./reports/screenshots/01-blackhole-singularity-readiness.png, ./reports/screenshots/02-blackhole-three-singularity-real-blackhole-three.png
- 로그 파일: ./reports/logs/01-blackhole-singularity-readiness.log, ./reports/logs/02-blackhole-three-singularity-real-blackhole-three.log
- raw json: ./reports/raw/01-blackhole-singularity-readiness.json, ./reports/raw/02-blackhole-three-singularity-real-blackhole-three.json
- 배포 URL: https://ai-webgpu-lab.github.io/exp-blackhole-three-singularity/
- 관련 이슈/PR: -
