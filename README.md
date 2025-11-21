# Difuzia Căldurii într-un Microprocesor (Simulare 1D, 2D, 3D)

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![NumPy](https://img.shields.io/badge/Library-NumPy-orange)
![Matplotlib](https://img.shields.io/badge/Library-Matplotlib-green)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

Acest proiect studiază și modelează numeric dispersia căldurii într-un microprocesor, utilizând **Metoda Diferențelor Finite (FDM)**. Simularea pornește de la un model simplificat 1D și scalează până la un model complex 3D, inspirat de arhitectura procesorului **Intel 8086** și de provocările termice ale procesoarelor moderne.

## 👥 Autori
**Grupa 164**
* **Soisun Mina-David**
* **Jianu Toma**
* *Coordonator Științific / Curs: Bucătaru Mihai* 

---

## 📝 Descrierea Proiectului

Odată cu creșterea puterii de calcul, gestionarea căldurii a devenit critică. Acest proiect implementează rezolvarea numerică a ecuațiilor diferențiale parțiale (PDE) care guvernează transferul termic, analizând distribuția temperaturii $u(x,y,z)$ într-un domeniu $\Omega$.

Proiectul este împărțit în trei etape majore:
1.  **Modelul 1D:** Validarea metodei pe un fir cu conductivitate variabilă $k(x)$.
2.  **Modelul 2D:** Simulare pe o suprafață pătratică (vedere "top-down" a chip-ului), cu sursă de căldură centrală. Include optimizări folosind **noduri fictive** pentru condițiile Neumann.
3.  **Modelul 3D:** Simulare volumetrică ce permite analiza poziționării sursei de căldură pe axa Z (simulând delidding-ul și contactul direct cu stratul de siliciu).

## 🧮 Model Matematic

Ecuația generală de difuzie (stare staționară) utilizată este:

$$-\nabla \cdot (k(\mathbf{x}) \nabla u(\mathbf{x})) = f(\mathbf{x})$$

Unde:
* $\Omega$ este domeniul de studiu.
* $u$ este temperatura.
* $k$ este tensorul conductivității termice (variabil spațial).
* $f$ este sursa internă de căldură.

### Condiții la Frontieră
* **Dirichlet ($\Gamma_D$):** Temperatură impusă la margini ($u = g_D$).
* **Neumann ($\Gamma_N$):** Flux termic impus (izolație), $\frac{\partial u}{\partial n} = 0$.

## 🚀 Funcționalități și Implementare

### 1. Simulare 1D
* Rezolvarea sistemului tridiagonal.
* Conductivitate neconstantă: $k(x) = x + 1$.
* Verificare cu soluția exactă $u_{exact}(x) = \sin(\pi x)$.

### 2. Simulare 2D
* Discretizare pe grilă $N \times N$.
* Implementarea condițiilor Neumann folosind **Metoda Nodurilor Fictive** pentru a crește ordinul de convergență de la $O(h)$ la $O(h^2)$ sau chiar $O(h^3)$.
* Vizualizare prin *Heat Maps* (hărți de temperatură).

### 3. Simulare 3D
* Extindere la volum cubic.
* **Feature special:** Posibilitatea de a muta sursa de căldură pe axa Z ($z=0.5, z=0.75, z=0.9$) pentru a studia efectul apropierii sursei de sistemul de răcire.
* Vizualizare folosind *Scatter plots* 3D și secțiuni plane.

## 📊 Rezultate și Convergență

Proiectul include o analiză detaliată a erorilor:
* Calculul erorii maxime și a erorii $L_2$.
* Grafice **Log-Log** pentru demonstrarea ordinului de convergență.
* S-a demonstrat că utilizarea nodurilor fictive și medierea coeficienților la interfețe îmbunătățește semnificativ precizia numerică.


<img width="2050" height="852" alt="grafice solutii 2D O(h^3)" src="https://github.com/user-attachments/assets/6802c1c4-5852-46e5-9ae6-0ff5b05d4fef" />

<img width="721" height="658" alt="3D_N+D_sol exacta" src="https://github.com/user-attachments/assets/f37d4177-0090-4d65-a5ab-4a0028717cbe" />

<img width="721" height="658" alt="3D_N+D_sol numerica" src="https://github.com/user-attachments/assets/1f988a8f-a77b-40aa-aa8b-432c29fc2fc4" />

## 🛠️ Instalare și Rulare

Pentru a rula scripturile, ai nevoie de Python instalat și de următoarele biblioteci:

```bash
pip install numpy matplotlib
