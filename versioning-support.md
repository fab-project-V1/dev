Versioning and Support Policy
Fabric follows semantic versioning (SemVer) and a tiered support lifecycle for long-term stability and upgrade clarity.

📌 Versioning Scheme
Format: MAJOR.MINOR.PATCH

MAJOR: Breaking changes (e.g., DSL runtime redesign)

MINOR: Backward-compatible feature additions (e.g., new agents or APIs)

PATCH: Backward-compatible bug fixes or compliance updates

Example: 1.3.2

🔁 Release Cadence
Release Type	Frequency	Notes
Major	~Every 12 months	Introduces system-wide changes
Minor	~Every 3 months	Adds new features, integrations
Patch	Bi-weekly/monthly	Focused on fixes and stability

📦 Supported Versions
Current (LTS): Full support, bug fixes, security patches.

Previous (N-1): Security updates only.

Older: Deprecated unless under extended commercial support.

🛠️ Upgrade Guidance
Patch updates are safe drop-ins.

Minor updates may require CLI or module upgrade (fab upgrade).

Major upgrades include migration tools/scripts under /tooling/migration.

📬 Deprecation Notices
Deprecated features are flagged in changelogs and CLI warnings.

Minimum 1 release cycle notice before full removal.

