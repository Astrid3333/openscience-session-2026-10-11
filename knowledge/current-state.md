# Current State

- Goal: dominio `rig` completo (29 actions) + mocap Astra→MetaHuman funcional en `/home/astrid/unreal-mcp`.
- Stage: tools MetaHuman verificadas contra BP_Fei real (spawnado en `/Temp/Untitled_1`); proyecto mocap (`fei_mocap.py`) corregido y verificado end-to-end sin cámara.
- Commits unreal-mcp: `60a44d4`, `bb93e77`, `c07b187` (11 MetaHuman), `6e34945` (FindActorForRig label + fei_mocap.py).
- Editor: abierto (socket 55557); el .so de `6e34945` necesita reinicio de editor para el fix de label (el pipeline no lo necesita: usa nombre interno exacto resuelto por `find_fei()`).
- fei_mocap.py: find_fei dinámico + drive via tools batch (set_actor_transform / set_morph_targets / set_rig_pose); controles FK del rig stock (`*_fk_ctrl`); morphs con prefijo `head_lod0_mesh__`.
- Para correr: `/home/astrid/unreal-mcp/Python/.venv/bin/python fei_mocap.py` (el python del sistema no tiene cv2/mediapipe).
- Postergado: fei_bone_test.py / live_pose_*.py (scripts legacy para CR_FeiBody, sin cablear a tools).
