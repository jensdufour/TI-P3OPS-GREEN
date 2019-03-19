# Testplan Zulu1
### Auteur(s): 
- Kenzie Coddens
- Maximilian Leire

## Alle te testen onderdelen onderverdeeld in secties:
- IP-adres: 172.16.0.69
- Subnet-mask: 255.255.255.252
- Default gateway: 172.16.0.70
- [ ] Vanuit LAN interface ping op `172.16.0.70` werkt.
### Test 1: Testscript (portscan)
- [ ] Voer het testscript portscan.sh uit vanop een externe server naar een interne server en kijk welke poorten allemaal open staan.
- [ ] Voer het testscript portscan.sh uit vanop een interne server naar een externe server en kijk welke poorten allemaal open staan.
### Test 2: Testen van uitgaand verkeer
- [ ] Een interne server kan naar een externe server pingen zoals `1.1.1.1`.
- [ ] Er kan naar buiten gesurft worden vanop interne hosts/servers.

### Test 3: Testen van binnenkomend verkeer
- [ ] Er kan van buitenaf via SSH met een server verbonden worden.
- [ ] Er kan van buitenaf naar de interne webserver gesurft worden.
- [ ] Een interne server kan succesvol een mail naar red.local sturen.
- [ ] Er kan van buitenaf naar de interne fileserver gesurft worden.