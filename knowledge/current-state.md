# Current State

- Goal: dominio `rig` completo en el MCP de Unreal (`/home/astrid/unreal-mcp`): 29 actions = 18 rigging base + `set_rig_pose` batch + 11 MetaHuman (morphs/anim/grooms/LODSync) para mocap Astra Pro → MetaHuman.
- Stage: código + build + docs completos. Commits: `60a44d4` (18 actions), `bb93e77` (set_rig_pose), `c07b187` (11 MetaHuman + HairStrands). `.so` compilado 2026-10-12 00:14, aún no cargado (editor apagado).
- Current task: esperando que el usuario abra el editor Unreal (socket 55557) para smoke test conjunto rig + MetaHuman.
- Next action: listar tools (`rig_*` = 29), smoke test (find_rig_assets, spawn_skeletal_actor, list_rig_controls, list_morph_targets, set_lod_sync…) y cerrar el ciclo.
- Postergado: cablear fei_mocap.py/fei_bone_test.py de execute_python a `rig_set_rig_pose`.
