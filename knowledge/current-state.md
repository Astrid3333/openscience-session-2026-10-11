# Current State

- Goal: dominio `rig` completo (29 actions) + mocap Astra→MetaHuman funcional en `/home/astrid/unreal-mcp`.
- Stage: **mocap cuerpo+cara verificado en vivo** — body skeleton (10 huesos world-space aim via set_rig_pose) 16-20 updates/s 0 fallos + actor transform + face morphs. Pipeline completo.
- Commits unreal-mcp: `60a44d4`, `bb93e77`, `c07b187` (11 MetaHuman), `6e34945` (FindActorForRig label + fei_mocap.py), `4a493a8` (fei_bone_test + live_pose_* + .gitignore), `61e0cd1` (retarget 3D cuerpo).
- Editor: abierto (socket 55557); nivel `/Temp/Untitled_1` SIN guardar — no reiniciar sin pedirlo. El .so de `6e34945` necesita reinicio para el fix de label C++ (pipeline no lo necesita: resuelve nombre interno por `find_fei()`).
- BP_Fei: nombre interno `BP_Fei_C_UAID_408D5C334E90430A03_2037143183` (cambia por spawn). Rig stock; pose de reposo NO es [0,0,0] — restaurar con `reset_rig_controls`. Rest-world de 10 huesos clave calibrado al arrancar (get_rig_bone space=world tras reset).
- Convención de espacios del rig stock: controls en `space='rig'` (NO 'component'); bones world via `set_rig_pose` con `space='world'` (batch de huesos, un solo round-trip TCP).
- fei_mocap.py: retarget 3D — quaternion/euler UE via matrices (roundtrip exacto), _aim_quat (local +X hueso -> dir world, verificado dot=1.0 vs editor), mp_to_ue=(-x,-z,y) para usuario frente a cámara. 10 huesos: upperarm/lowerarm/thigh/calf l+r, spine_03, head.
- Cámara: Orbbec Astra Pro (2bc5:0501) en /dev/video0, 640x480; DISPLAY=:0 X11. Face intermitente en sala oscura. Para correr: `timeout -s INT 45 .venv/bin/python -u fei_mocap.py`.
- Astra Pro depth: activada con SDK OpenNI de Orbbec 2.3.0.86 (runtime en unreal-mcp/Python/astra_depth/). depth_cap helper C++ stream 640x480@30. fei_mocap.py usa DepthStream.sample() en cadera media → dist_m real para drive_fei_actor (eje Y UE). Prueba run3: 30fps, d=2.43-2.47m, body_ok=16-18/s, body_fail=0. Commit unreal-mcp `f948035`.
