# Current State

- Goal: implementar el dominio `rig` (18 actions de rigging) en el MCP de Unreal (`/home/astrid/unreal-mcp`): skeleton/sockets/actores skeletal + controles Control Rig.
- Stage: código + build + docs completos; commit `60a44d4` en unreal-mcp. Falta reinicio del editor por el usuario y verificación de tools.
- Current task: esperando reinicio del editor Unreal para smoke test del dominio rig.
- Next action: tras el reinicio, listar tools (`rig_*`), ejecutar smoke test (find_rig_assets, spawn_skeletal_actor, list_rig_controls) y cerrar el ciclo.
