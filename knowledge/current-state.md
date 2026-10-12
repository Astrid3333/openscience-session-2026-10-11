# Current State

- Goal: dominio `rig` completo (29 actions) + mocap Astra→MetaHuman funcional en `/home/astrid/unreal-mcp`.
- Stage: **pipeline mocap verificado en vivo con Astra Pro** — body (actor transform) 8-10 updates/s 0 fallos; face (morphs) intermitente según luz/distancia. Dominio rig completo (29 actions) + todos los scripts commiteados.
- Commits unreal-mcp: `60a44d4`, `bb93e77`, `c07b187` (11 MetaHuman), `6e34945` (FindActorForRig label + fei_mocap.py), `4a493a8` (fei_bone_test + live_pose_* + .gitignore).
- Editor: abierto (socket 55557); nivel `/Temp/Untitled_1` SIN guardar — no reiniciar sin pedirlo. El .so de `6e34945` necesita reinicio para el fix de label C++ (pipeline no lo necesita: resuelve nombre interno por `find_fei()`).
- BP_Fei: nombre interno `BP_Fei_C_UAID_408D5C334E90430A03_2037143183` (cambia por spawn), loc (0,200,100). Rig stock (149 controles `*_fk_ctrl`); pose de reposo NO es [0,0,0] en piernas/brazos — restaurar con `reset_rig_controls` (151 controles).
- Convención de espacios del rig stock: controls en `space='rig'` (NO 'component', compone mal); bones en `space='component'`.
- fei_mocap.py: find_fei dinámico + drive via tools batch (set_actor_transform / set_morph_targets / set_rig_pose); morphs con prefijo `head_lod0_mesh__`.
- fei_bone_test.py: test procedural 20 controles, sin cámara, reset con reset_rig_controls. live_pose_to_ue.py/live_pose_test.py: puente Astra→MediaPipe→UE, sin cámara no probados en vivo.
- Cámara: Orbbec Astra Pro (2bc5:0501) en /dev/video0, 640x480; DISPLAY=:0 X11. Detección facial intermitente en sala oscura (acercarse/más luz mejora). fps ~30→15 con ambos landmarkers en CPU.
- Para correr: `timeout -s INT 45 .venv/bin/python -u fei_mocap.py` (python del sistema sin cv2/mediapipe; -u evita perder prints con timeout).
