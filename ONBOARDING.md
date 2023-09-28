# MDE onboarding

Things to consider when onboarding

Devices joined or managed:
- Onprem AD or workgroup
- Azure AD
- Operating system version
- SCCM
- Intune

## 3rd party AV

## Network requirements

- [MDE URLS](https://download.microsoft.com/download/6/b/f/6bfff670-47c3-4e45-b01b-64a2610eaefa/mde-urls-commercial.xlsx)

## Services

Windows diagnostics service must be enabled and auto start

Validate
```
sc qc diagtrack
```

Configure:
```
sc config diagtrack start=auto
```

# Servers