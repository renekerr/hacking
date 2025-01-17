## Reconocimiento Pasivo

### Descargar favicon y calcular su hash MD5
```
curl https://static-labs.tryhackme.cloud/sites/favicon/images/favicon.ico | md5sum
```
Este comando no interactúa directamente con el sistema objetivo, solo descarga un recurso público.

## Reconocimiento Activo

### Enviar solicitud GET con salida detallada
```
curl http://10.10.245.129/ -v
```

### Descubrir contenido web con FFUF
```
ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -u http://10.10.245.129/FUZZ
```

### Escanear contenido web con DIRB
```
dirb http://10.10.245.129/ /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
```

### Fuerza bruta de directorios con Gobuster
```
gobuster dir --url http://10.10.245.129/ -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
```
