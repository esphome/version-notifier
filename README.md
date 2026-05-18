# ESPHome Version Notifier

Internal tool that receives notifications of new ESPHome releases and fans out the version update to downstream repositories.

The release workflow in `esphome/esphome` dispatches [`notify.yml`](.github/workflows/notify.yml) once per release. Subscriber workflows in this repo react via `workflow_run` to do the actual work:

- [`update-firmware-repos.yml`](.github/workflows/update-firmware-repos.yml) — opens version-bump PRs in the firmware repos listed in [`repos.json`](repos.json) (stable releases only).
- [`trigger-ha-addon.yml`](.github/workflows/trigger-ha-addon.yml) — dispatches `bump-version.yml` in `esphome/home-assistant-addon`.
- [`trigger-schema.yml`](.github/workflows/trigger-schema.yml) — dispatches `generate-schemas.yml` in `esphome/esphome-schema`.

Adding a new downstream target is a new subscriber workflow here — no changes needed in `esphome/esphome`.
