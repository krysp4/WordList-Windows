# ad_usernames.txt — Kerberos / Active Directory Username Wordlist

## Descripción

`ad_usernames.txt` es una wordlist de **9,368,869 nombres de usuario únicos** generada y curada específicamente para la enumeración de usuarios en entornos **Active Directory** y ataques/auditorías **Kerberos**.

Todos los usuarios han sido:
- **Normalizados** (sin tildes, sin mayúsculas)
- **Filtrados** (solo caracteres válidos para AD: `a-z`, `0-9`, `.`, `-`, `_`)
- **Deduplicados** completamente

---

## Contenido

| Categoría | Ejemplos | Entradas aprox. |
|-----------|----------|-----------------|
| Nombres de usuario estadísticamente probables | `john.smith`, `jsmith`, `smithj` | ~1.8M |
| Usuarios de filtraciones reales (xato-net 10M) | `shadow`, `darkwing`, `m.garcia` | ~8M |
| Nombres corporativos en español | `a.garcia`, `garcia.ana`, `agarcia` | ~456K |
| Cuentas de servicio típicas | `svc.admin`, `svc.backup`, `svc.sql` | ~3.1K |
| Cuentas de administración | `administrator`, `domainadmin`, `itadmin` | incluido |
| Cuentas de aplicación | `svc.exchange`, `svc.iis`, `svc.sharepoint` | incluido |
| Cuentas departamentales | `hr.admin`, `finance`, `helpdesk` | incluido |
| Variaciones numéricas corporativas | `john1`, `jsmith01`, `admin2024` | incluido |
| Usuarios de honeypots SSH reales | capturados de ataques reales | ~26K |
| Defaults MSSQL / SAP | `sa`, `sap*`, `mssql*` | incluido |

---

## Fuentes

| Repositorio | Descripción |
|-------------|-------------|
| [SecLists - danielmiessler](https://github.com/danielmiessler/SecLists) | xato-net 10M, nombres, defaults, español, honeypots, credenciales |
| [statistically-likely-usernames - insidetrust](https://github.com/insidetrust/statistically-likely-usernames) | jsmith, john.smith, johnsmith, smithj, top-formats |
| [common-ad-usernames - crypt0rr](https://github.com/crypt0rr/common-ad-usernames) | Usuarios comunes en AD reales |
| [Active-Directory-Wordlists - Cryilllic](https://github.com/Cryilllic/Active-Directory-Wordlists) | Lista específica AD |

---

## Patrones de usuario incluidos

```
nombre.apellido     →  ana.garcia
nombreapellido      →  anagarcia
apellido.nombre     →  garcia.ana
apellidonombre      →  garciaana
n.apellido          →  a.garcia
napellido           →  agarcia
apellido.n          →  garcia.a
nombre-apellido     →  ana-garcia
nombre_apellido     →  ana_garcia
nombre solo         →  ana
apellido solo       →  garcia
+ variaciones numéricas: ana.garcia1, agarcia01, ana.garcia2025...
```

---

## Uso recomendado

### Kerbrute (AS-REP Roasting / enumeración sin credenciales)
```bash
kerbrute userenum --dc <IP_DC> -d <dominio.local> ad_usernames.txt
```

### CrackMapExec (SMB user enumeration)
```bash
crackmapexec smb <IP> -u ad_usernames.txt -p '' --no-bruteforce
```

### Impacket GetNPUsers (AS-REP Roasting)
```bash
GetNPUsers.py <dominio>/ -usersfile ad_usernames.txt -dc-ip <IP_DC> -no-pass
```

### Spray de contraseñas (¡cuidado con el lockout!)
```bash
kerbrute passwordspray --dc <IP_DC> -d <dominio.local> ad_usernames.txt 'Password2024!'
```

---

## Estadísticas del archivo

```
Archivo      : ad_usernames.txt
Entradas     : 9,368,869 usuarios únicos
Tamaño       : 102.55 MB
Encoding     : UTF-8
Formato      : Un usuario por línea, sin cabeceras
Caracteres   : [a-z0-9.\-_] únicamente
Generado con : ad_user_enum_gen.py (v2)
```
