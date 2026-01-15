# Migration Guide: report_wkhtmltopdf_param

## Migration from V18 to V19

### Date: January 2026

---

## Summary of Changes

This document summarizes the migration of the `report_wkhtmltopdf_param` module from Odoo 18.0 to 19.0, following the [OCA Migration Guidelines](https://github.com/OCA/maintainer-tools/wiki/Migration-to-version-19.0).

### Version Changes

| Field | V18 | V19 |
|-------|-----|-----|
| Module Version | 18.0.1.0.1 | 19.0.1.0.0 |
| Odoo Version | 18.0 | 19.0 |

---

## Changes Performed

### 1. Module Manifest (`__manifest__.py`)

- **Version bumped**: Changed from `18.0.1.0.1` to `19.0.1.0.0`
- No changes were needed in dependencies (still depends on `web`)
- License and metadata remain unchanged

### 2. Documentation Updates (`README.rst`)

- Updated all OCA repository links from `18.0` to `19.0`
- Updated Weblate translation links
- Updated Runboat links for testing
- Updated Bug Tracker feedback links

### 3. Credits (`readme/CREDITS.md`)

- Removed references to past migration sponsorships (as per OCA guidelines)

### 4. Python Code Review

The following Odoo 19.0 migration patterns were checked:

| Pattern | Status | Notes |
|---------|--------|-------|
| `self._cr` → `self.env.cr` | ✅ Not present | No changes needed |
| `self._uid` → `self.env.uid` | ✅ Not present | No changes needed |
| `self._context` → `self.env.context` | ✅ Not present | No changes needed |
| `odoo.osv.expression` → `odoo.fields.Domain` | ✅ Not present | No changes needed |
| `_sql_constraints` → `models.Constraint` | ✅ Not present | No changes needed |
| `auto_join` → `bypass_search_access` | ✅ Not present | No changes needed |
| `read_group` → `_read_group`/`formatted_read_group` | ✅ Not present | No changes needed |
| Controller `type="json"` → `type="jsonrpc"` | ✅ Not present | No controllers in module |
| `groups_id` → `group_ids` | ✅ Not present | No changes needed |

### 5. XML Views Review

- Checked for `groups_id` usage (requires change to `group_ids` in V19)
- No changes were necessary - views are compatible with V19

### 6. Tests

- Tests are compatible with V19
- Using `@tagged("post_install", "-at_install")` decorator
- No deprecated patterns found

---

## Module Functionality (Unchanged)

This module continues to provide the following functionality:

1. **Custom wkhtmltopdf Parameters**: Allows adding custom command-line parameters to wkhtmltopdf when generating PDF reports
2. **Paper Format Extension**: Extends `report.paperformat` model with a `custom_params` One2many field
3. **Parameter Validation**: Validates parameters by attempting to generate a sample PDF

---

## Technical Considerations

### Dependencies

- **`web`**: Required dependency (unchanged)

### Security

- Access rights defined in `security/ir.model.access.csv` remain unchanged
- Portal users: read only
- Regular users: read, create
- System administrators: full access

### Data Models

| Model | Description |
|-------|-------------|
| `report.paperformat.parameter` | Stores custom wkhtmltopdf parameters |
| `report.paperformat` (inherited) | Extended with `custom_params` field |
| `ir.actions.report` (inherited) | Extended `_build_wkhtmltopdf_args` method |

---

## Post-Migration Checklist

- [ ] Run module tests: `odoo-bin -c odoo.conf -i report_wkhtmltopdf_param --test-enable`
- [ ] Verify PDF generation with custom parameters
- [ ] Check paper format configuration in UI (Settings > Technical > Reports > Paper Format)
- [ ] Verify existing custom parameters are preserved after migration

---

## OCA Guidelines Compliance

This migration follows the [OCA Migration to version 19.0](https://github.com/OCA/maintainer-tools/wiki/Migration-to-version-19.0) guidelines:

- ✅ Version bumped to `19.0.1.0.0`
- ✅ No migration scripts from previous versions (none existed)
- ✅ Removed past migration sponsorship references in CREDITS.rst
- ✅ Checked all V19-specific code changes
- ✅ Documentation updated with version 19.0 references

---

## References

- [OCA Migration Guide V19](https://github.com/OCA/maintainer-tools/wiki/Migration-to-version-19.0)
- [Odoo 19.0 Coding Guidelines](https://www.odoo.com/documentation/19.0/contributing/development/coding_guidelines.html)
- [OCA Conventions](https://odoo-community.org/page/contributing)

---

## Contributors

Migration performed following OCA community standards.
