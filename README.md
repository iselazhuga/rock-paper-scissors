## Metodologjia e Mbledhjes së të Dhënave

### Përzgjedhja e Variablave

Fillimisht konsideruam shumë variacione të mundshme, por përfshirja e të gjithave do të krijonte shumë skenarë dhe do të kërkonte një sasi të pamenaxhueshme imazhesh. Prandaj, u fokusuam në tre variabla kryesore që kanë ndikim të drejtpërdrejtë në atë që modeli mund të mësojë:

* **Gjinia:** djalë / vajzë
* **Ana e dorës:** përpara / mbrapa
* **Këndi:** drejt / majtas / djathtas

Kjo krijon gjithsej **2 × 2 × 3 = 12 skenarë**.

Variablat e tjera u hoqën sepse mbivendoseshin me variablat e përzgjedhura, ndikoheshin natyrshëm nga kushte të tjera, ose kërkonin shumë të dhëna shtesë.

| Variabla e hequr    | Arsyeja                                                                                                          |
| ------------------- | ---------------------------------------------------------------------------------------------------------------- |
| Madhësia e dorës    | Ka pak ndryshim real me vetëm dy kontribues; distanca nga kamera ndikon gjithashtu në madhësinë e dorës në foto. |
| Ngjyra e sfondit    | Mund të ndryshojë natyrshëm gjatë mbledhjes së të dhënave.                                                       |
| Kontrasti           | Ndikohet kryesisht nga ndriçimi dhe sfondi.                                                                      |
| Pozicioni/kompozimi | Lidhet me distancën dhe pozicionimin e dorës.                                                                    |
| Modeli i kamerës    | Do të shtonte shumë kombinime pa përfitim të qartë.                                                              |
| Ora e ditës         | Ndikon kryesisht te ndriçimi.                                                                                    |
| Dhoma               | Ndikon kryesisht te sfondi dhe ndriçimi.                                                                         |

### Zgjerimi Artificial i të Dhënave (Augmentimi)

Për të reduktuar punën manuale, fotot origjinale u morën vetëm me **dorën e djathtë**. Më pas përdorëm **horizontal flip** për të krijuar shembuj të dorës së majtë.

Përdorëm gjithashtu rrotullime artificiale prej **90°, 180° dhe 270°** për të krijuar shembuj shtesë.

Nga **216 imazhe origjinale**, u krijuan rreth **1,728 imazhe** pas këtyre transformimeve.

Ndryshe nga *flip*-i horizontal, rrotullimet artificiale mund të krijojnë pozicione që nuk përfaqësojnë mënyrën tipike se si një dorë mbahet përpara kamerës. Prandaj, ndikimi i tyre u testua në vend që të supozohej se do të përmirësonte modelin.

### Krahasimi i të Dhënave

Trajnuam dhe krahasuam dy modele:

1. **Vetëm me imazhet reale** — 216
2. **Me imazhet reale + të augmentuara** — 1,728

Në këtë mënyrë mundëm të vlerësonim nëse augmentimi përmirëson apo dëmton performancën e modelit.

Modeli përfundimtar do të zgjidhet bazuar në performancën e tij në një **set testimi të veçuar**, i cili nuk është përdorur gjatë trajnimit. Kjo është më e rëndësishme sesa performanca vetëm në të dhënat e trajnimit, pasi një rezultat shumë i lartë në trajnim mund të tregojë **overfitting**.

### Testimi dhe Përmirësimi

Pas trajnimit, modeli u testua me imazhe të reja. Analizuam gabimet dhe, kur identifikuam një problem të caktuar, shtuam imazhe specifike për ta adresuar.

Për shembull, nëse modeli ngatërron **gërshërët me gurin**, mund të shtojmë më shumë imazhe të gërshërëve me gishtat më të hapur.

**Cikli:** Mbledhje → Augmentim → Trajnim → Testim → Përmirësim → Ri-trajnim

### Rezultatet pas Testimit

*Do të plotësohet pas përfundimit të Step 6.*

* **Çfarë vërejtëm:** ...
* **Problemi:** ...
* **Ndryshimi:** ...
* **Rezultati:** ...
* **Reale vs. Reale + Augmentuar — cili performoi më mirë:** ...
