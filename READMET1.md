
<img width="300" height="250" alt="P4 foto logo" src="https://github.com/user-attachments/assets/4e35380b-6401-4ff6-9139-b76db478638f" />

# T01: DRP: còpies de seguretat. Estudi cas, client (treball cooperatiu) 


## EXPLICACIÓ

### Introducció
La primera hora el vostre responsable de seguretat us presenta el tema de les còpies de seguretat a partir d’un material didàctic. A continuació, caldrà que hi treballeu els aspectes del tema i ho fareu mitjançant una dinàmica cooperativa.

### Presentació del cas client
"Muntatges i Serveis Tècnics SL" és una petita empresa dedicada a la instal·lació i manteniment d'equips industrials.

#### Infraestructura Tècnica:
- **Servidor de Fitxers (Ubuntu Server):** Conté tota la documentació crítica:
  - Documents de Projectes: Plànols, especificacions tècniques (300 GB, creixement moderat).
  - Bases de Dades (Comptabilitat i Clients): Crítiques i d'ús diari (20 GB, canvi constant).
  - Carpetes Personals dels Usuaris: Per a la feina diària (100 GB).
- **10 Equips Clients (Windows 10/11):** Els usuaris treballen majoritàriament amb fitxers del servidor, però alguns tècnics guarden de forma temporal informes i altres arxius importants a la carpeta Documents.
- **Connexió a Internet:** Fibra òptica de 600 Mbps (simètrica).

#### Requisits de Recuperació:
- **Temps de Recuperació (RTO):** Les dades de Comptabilitat/Clients han d'estar disponibles en menys de 4 hores.
- **Pèrdua de Dades Admesa (RPO):** Es pot admetre una pèrdua màxima de 24 hores per a la majoria de dades, però les dades de Comptabilitat/Clients no poden perdre més de 4 hores de treball.
- **Retenció:** Cal guardar les dades amb un historial d'almenys un més.

---

## EXERCICIS

### Fase 1: Treball individual
De forma individual, heu de donar resposta a les següents preguntes basant-se en el cas pràctic:

#### 1. Què copiar? (Priorització)
Les dades més crítiques del servidor són, en primer lloc, les bases de dades de comptabilitat i clients, ja que són essencials per al funcionament diari de l’empresa. Aquestes dades no poden perdre més de quatre hores de treball i han d’estar disponibles ràpidament en cas de fallada, per això tenen la màxima prioritat.  

En el cas dels 10 equips, clients, no cal fer còpia completa de tots els equips, ja que la majoria de les dades es troben al servidor. Tanmateix, alguns tècnics guarden informació temporal important a la carpeta Documents.  

**Ordre de prioritat per fer còpies:**
1. Bases de dades de comptabilitat i clients.
2. Documents de projectes.
3. Carpetes personals dels usuaris.
4. Carpeta Documents dels equips clients només si contenen dades crítiques no al servidor.

#### 2. Periodicitat i Tipus de Còpia
**Bases de dades (Comptabilitat i Clients)**  
- Diàries: Incrementals cada 4 h per complir RPO de 4 h.  
- Setmanals: Complet diumenge.  
**Raó:** Dades molt crítiques, necessiten recuperació ràpida per RTO < 4 h.

**Documents de projectes**  
- Diàries: Diferencials a final de jornada.  
- Mensuals: Completa al final del mes.  
**Raó:** Dades importants per projectes; pèrdua d’un dia és tolerable.

**Carpetes personals dels usuaris**  
- Diàries: Incrementals al final del dia.  
- Setmanals: Complet diumenge.  
**Raó:** Permet recuperar treball diari sense ocupar molt espai.

**Carpeta Documents dels equips clients amb dades crítiques**  
- Diàries: Incrementals o sincronització automàtica.  
**Raó:** Només per dades que no estan al servidor, per evitar pèrdues.

#### 3. Mitjans i Ubicació
**Mitjans i Ubicació (Regla 3-2-1)**  
- **Mitjans de còpia:**  
  - NAS intern: còpies diàries per recuperació ràpida.  
  - Disc dur extern / cintes: còpies setmanals/mensuals guardades fora de l’oficina.  
  - Cloud: còpies crítiques fora del lloc per emergències.  
- **Ubicació:**  
  - Còpia recent: al NAS intern.  
  - Còpia fora de l’oficina: disc dur extern o Cloud.  

**Resum regla 3-2-1:**  
- 3 còpies de les dades  
- 2 tipus de mitjà diferents  
- 1 còpia fora del lloc

---

### Fase 2: Treball per parelles
1. **Discussió i Consens:** Comparen les seves respostes individuals (Fase 1).  
2. **Elaboració d'una Proposta Unificada:** Heu de consensuar i dissenyar el vostre propi Esquema 3-2-1 de Còpies (3 còpies, 2 mitjans, 1 fora de lloc) basat en els requisits del cas.

| Element                | Proposta de la Parella                       | Justificació                                                                 |
|------------------------|--------------------------------------------|----------------------------------------------------------------------------|
| Dades Crítiques        | Bases de dades de Comptabilitat i Clients | Són essencials per al funcionament diari, RPO ≤ 4 h i RTO < 4 h.           |
| Periodicitat (BD)      | Diàries (incrementals cada 4 h) i setmanals (completa diumenge) | Incrementals diàries per minimitzar la pèrdua de dades; completa setmanal per tenir còpia íntegra. |
| Tipus de Còpia (BD)    | Incremental diària + completa setmanal      | Permet restauració ràpida i optimitza espai.                                |
| Mitjà 1 (Local)        | NAS intern                                   | Còpia recent per restauració ràpida dins de l’empresa.                     |
| Mitjà 2 (Extern)       | Disc dur extern / Cloud fora de l’oficina   | Garantir seguretat fora del lloc en cas d’incident físic; cumpleix regla 3-2-1. |

---

### Fase 3: Treball en grup
1. **Debat i Selecció:** Cada parella presenta el seu esquema. El grup debat els pros i contres de cada proposta (cost, temps de recuperació, seguretat, simplicitat).  
2. **Disseny de la Política Final:** El grup ha de redactar la Política de Còpies de Seguretat Definitiva que presentaran a l'empresa "Muntatges i Serveis Tècnics SL".

#### Document Final

##### 1) Dades Objecte de Còpia
**Servidor Ubuntu Server:**  
- Bases de dades Comptabilitat/Clients (20 GB) → crítiques → còpia diària incremental + setmanal completa  
- Documents de Projectes (300 GB) → importants → còpia diària diferencial + còpia completa mensual  
- Carpetes personals dels usuaris (100 GB) → moderadament crítiques → còpia diària incremental + còpia completa setmanal  

**Equips Clients (Windows 10/11):**  
- Carpeta Documents amb arxius temporals crítics → còpia diària incremental o sincronització amb servidor

##### 2) Cronograma Setmanal Detallat

| Dia       | Dades                         | Tipus de còpia                  | Mitjà                        |
|-----------|-------------------------------|--------------------------------|------------------------------|
| Dilluns   | Bases de dades                | Incremental                    | NAS intern                   |
| Dimarts   | Documents de Projectes        | Diferencial                     | NAS intern                   |
| Dimecres  | Carpetes personals            | Incremental                    | NAS intern                   |
| Dijous    | Bases de dades                | Incremental                    | NAS intern                   |
| Divendres | Documents de Projectes        | Diferencial                     | NAS intern                   |
| Dissabte  | Carpetes personals            | Incremental                    | NAS intern                   |
| Diumenge  | Bases de dades (completa) + Documents de Projectes mensual) | Completa | NAS intern + Disc dur extern / Cloud |

**Resum:**  
Les dades crítiques com les bases de dades es copien incrementalment durant la setmana i completa el diumenge.  
Els documents de projectes i les carpetes personals es copien diferencial o incremental segons la importància, amb còpia completa mensual o setmanal.  
Les còpies diàries van al NAS intern i les completes a disc extern o Cloud, complint la regla 3-2-1.

##### 3) Elecció de Mitjans i Ubicació (Regla 3-2-1)
- **Mitjà 1 (Local):** NAS intern, per còpies ràpides i restauració immediata.  
- **Mitjà 2 (Extern):** Disc dur extern físic + Cloud (ex. Google Cloud o Azure) per còpies crítiques fora del lloc.  
- **Ubicació Fora de Lloc:**  
  - Disc dur extern guardat fora de l’oficina (ex. caixa de seguretat o domicili alternatiu).  
  - Cloud: gestionat pel proveïdor seleccionat (responsable: responsable IT de l’empresa).

##### 4) Estratègia de Recuperació (RTO/RPO)
- **RPO (Pèrdua de dades màxima):**  
  - Bases de dades: màxim 4 hores → garantides amb còpies incrementals cada 4 h.  
  - Altres dades: màxim 24 hores → assegurat amb còpies diàries diferencials/incrementals.  

- **RTO (Temps de recuperació):**  
  - Bases de dades: < 4 h → restauració des del NAS intern per velocitat; còpia externa només en cas de desastre major.  
  - Altres dades: restauració de NAS intern o Disc dur extern/Cloud segons necessitat, amb temps més flexible.  

**Justificació:** Aquesta estratègia garanteix seguretat, rapidesa en la recuperació i compliment dels requisits crítics de l’empresa, respectant la regla 3-2-1.

---

### Materials i links de suport
- Moodle 0226 Seguretat Informàtica. RA2.AA3Còpies  
- INCIBE. Copias de seguridad. Una guía de aproximación para el empresario.  
- Xataka. Backup 3 - 2 - 1, el método definitivo para mantener a salvo tus datos. [YouTube]. Setembre 2017. Disponible a:  
  https://youtu.be/PM_M4Iz6I4o?si=F7DRyDDTZE3hjWn8

