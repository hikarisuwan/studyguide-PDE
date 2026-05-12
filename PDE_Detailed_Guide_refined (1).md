# Detailed Step-by-Step PDE Study Guide (MATE95001)

This guide walks through every problem from both problem sheets and the lecture notes with full step-by-step reasoning. Every algebraic manipulation is shown. Every choice of method is justified. Read it slowly.

> **Refined version note.** This version has been edited to correct several mathematical caveats and sign-convention issues: the logarithmic harmonic function is stated with its singularity excluded; nonlinear "homogeneous" language is treated more carefully; the plucked-string ramp/triangle ambiguity is flagged; the infinite-square-well $E<0$ case is corrected; the Helmholtz Green's-function sign convention is clarified; and the Fourier-transform sign convention for Schrödinger's equation is explained.


---

## How to Use This Guide

Each problem is presented in this format:

1. **The problem** — what is being asked.
2. **What we know / what we need to find** — laying out the givens.
3. **Strategy** — *why* we choose the method we do.
4. **Step-by-step working** — every line of algebra, with commentary.
5. **Sanity checks** — verifying the answer makes sense.
6. **Pattern to remember** — what this problem teaches you for the next one.

---

# Part A — Foundations: ODEs, PDEs, Operators

## A.1 The Difference Between an ODE and a PDE

### A.1.1 Problem
Describe what is meant by:
- (i) An ordinary differential equation (ODE)
- (ii) A partial differential equation (PDE)
- (iii) Why do PDEs see more application than ODEs in applied natural sciences?

### A.1.2 Working through the definitions

**(i) ODE — Step by step.**

A differential equation is *any* equation involving a derivative. The "ordinary" in ODE refers to the type of derivative involved.

Recall that there are two kinds of derivatives:
- **Ordinary derivatives** like $\frac{du}{dx}$ — used when $u$ depends on only one variable, $x$.
- **Partial derivatives** like $\frac{\partial u}{\partial x}$ — used when $u$ depends on multiple variables and we differentiate with respect to one while holding the others fixed.

So an **ODE** is a differential equation that contains *only ordinary derivatives*. This automatically means the unknown function depends on only one independent variable. Examples:

$$\frac{du}{dx} = 3u \qquad \text{(first-order, } u \text{ depends only on } x\text{)}$$

$$\frac{d^2u}{dx^2} + 2\frac{du}{dx} + u = \sin x \qquad \text{(second-order)}$$

$$\left(\frac{du}{dx}\right)^3 + u^2 = x \qquad \text{(first-order, non-linear)}$$

**(ii) PDE — Step by step.**

A **PDE** is a differential equation that contains partial derivatives. This requires the unknown function to depend on more than one independent variable. In our course, we usually have $u = u(x, y, z, t)$ — three spatial dimensions and time. Examples:

$$3y^2 \frac{\partial u}{\partial x} + \frac{\partial u}{\partial y} = 2u$$

$$u\frac{\partial^2 u}{\partial x^2} + \left(\frac{\partial u}{\partial y}\right)^2 = u^2 + \left(\frac{\partial^4 u}{\partial x^4}\right)^{1/2}$$

**(iii) Why do PDEs dominate the natural sciences? Building the argument.**

Real physical phenomena rarely depend on just one variable. Consider these examples and ask "how many independent variables does each need?":

- **Temperature in a room.** The temperature at a corner near the radiator differs from the temperature near the window. So temperature depends on $x, y, z$ (where you are). It also changes during the day, so it depends on $t$. Total: 4 independent variables → must use a PDE.

- **Velocity of water in a river.** Different at the surface vs the bottom (depends on $z$), different near the bank vs the middle (depends on $y$), different upstream vs downstream (depends on $x$), changes during a flood (depends on $t$). 4 independent variables → PDE.

- **Wavefunction of an electron in an atom.** Depends on its 3D position and on time. 4 independent variables → PDE.

By contrast, an ODE could only describe extremely simple problems like the temperature of *a single point* over time, or the position of *a single particle* over time.

**The key insight:** PDEs are the natural mathematical language for *continuous fields* — anything that varies smoothly through space and time. Since most of physics, engineering, and applied science deals with such fields (heat, fluid flow, electromagnetic fields, quantum wavefunctions, mechanical stress in materials), PDEs are everywhere.

---

## A.2 The Three Standard Differential Operators

### A.2.1 Problem
Write the gradient $\nabla u$, divergence $\nabla \cdot \mathbf{u}$, and Laplacian $\nabla^2 u$ in Cartesian, cylindrical polar $(\rho, \phi, z)$, and spherical polar $(r, \theta, \phi)$ coordinates.

### A.2.2 Strategy

These are *standard formulas* — you don't derive them every time, you memorise them or look them up. But it's important to understand:
- **What each operator does** (acts on what, returns what).
- **Why the formulas in curvilinear coordinates have those extra factors** (they come from the metric, i.e. how distances are measured in those coordinates).

### A.2.3 The gradient $\nabla u$

**What it does:** Takes a *scalar* field $u(\mathbf{r})$ and returns a *vector* field. The vector points in the direction of steepest increase of $u$, with magnitude equal to the rate of increase in that direction.

**Cartesian** — the simplest case. Each component is the partial derivative in that direction:
$$\nabla u = \frac{\partial u}{\partial x}\,\hat{\mathbf{i}} + \frac{\partial u}{\partial y}\,\hat{\mathbf{j}} + \frac{\partial u}{\partial z}\,\hat{\mathbf{k}}.$$

**Cylindrical** $(\rho, \phi, z)$. The radial and $z$ directions behave like Cartesian, but the angular direction is different. Why? Because moving by $d\phi$ in the angular direction corresponds to a *physical* distance of $\rho\, d\phi$, not just $d\phi$. To get a derivative with respect to actual distance, we divide by $\rho$:
$$\nabla u = \frac{\partial u}{\partial \rho}\,\hat{\mathbf{e}}_\rho + \frac{1}{\rho}\frac{\partial u}{\partial \phi}\,\hat{\mathbf{e}}_\phi + \frac{\partial u}{\partial z}\,\hat{\mathbf{e}}_z.$$

**Spherical** $(r, \theta, \phi)$. Same logic: moving by $d\theta$ corresponds to physical distance $r\, d\theta$, so we divide by $r$. Moving by $d\phi$ at angle $\theta$ from the pole corresponds to physical distance $r \sin\theta\, d\phi$ (the radius of the circle of latitude), so we divide by $r\sin\theta$:
$$\nabla u = \frac{\partial u}{\partial r}\,\hat{\mathbf{e}}_r + \frac{1}{r}\frac{\partial u}{\partial \theta}\,\hat{\mathbf{e}}_\theta + \frac{1}{r\sin\theta}\frac{\partial u}{\partial \phi}\,\hat{\mathbf{e}}_\phi.$$

### A.2.4 The divergence $\nabla \cdot \mathbf{u}$

**What it does:** Takes a *vector* field $\mathbf{u}$ and returns a *scalar* field. Physically it measures the net outward flux per unit volume — how much the field is "spreading out" at a point.

**Cartesian:**
$$\nabla \cdot \mathbf{u} = \frac{\partial u_x}{\partial x} + \frac{\partial u_y}{\partial y} + \frac{\partial u_z}{\partial z}.$$

**Cylindrical:** The factors $\rho$ inside the derivative come from the volume element $dV = \rho\, d\rho\, d\phi\, dz$:
$$\nabla \cdot \mathbf{u} = \frac{1}{\rho}\frac{\partial(\rho u_\rho)}{\partial \rho} + \frac{1}{\rho}\frac{\partial u_\phi}{\partial \phi} + \frac{\partial u_z}{\partial z}.$$

**Spherical:** Volume element $dV = r^2 \sin\theta\, dr\, d\theta\, d\phi$:
$$\nabla \cdot \mathbf{u} = \frac{1}{r^2}\frac{\partial(r^2 u_r)}{\partial r} + \frac{1}{r\sin\theta}\frac{\partial(\sin\theta\, u_\theta)}{\partial \theta} + \frac{1}{r\sin\theta}\frac{\partial u_\phi}{\partial \phi}.$$

### A.2.5 The Laplacian $\nabla^2 u$

**What it does:** Takes a scalar, returns a scalar. By definition $\nabla^2 u = \nabla \cdot (\nabla u)$ — the divergence of the gradient. Physically it measures how much $u$ at a point differs from the *average* of $u$ in a small neighbourhood around it.

**Cartesian** — just three second derivatives:
$$\nabla^2 u = \frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2} + \frac{\partial^2 u}{\partial z^2}.$$

**Cylindrical:**
$$\nabla^2 u = \frac{1}{\rho}\frac{\partial}{\partial \rho}\left(\rho \frac{\partial u}{\partial \rho}\right) + \frac{1}{\rho^2}\frac{\partial^2 u}{\partial \phi^2} + \frac{\partial^2 u}{\partial z^2}.$$

**Spherical:**
$$\nabla^2 u = \frac{1}{r^2}\frac{\partial}{\partial r}\left(r^2 \frac{\partial u}{\partial r}\right) + \frac{1}{r^2 \sin\theta}\frac{\partial}{\partial \theta}\left(\sin\theta \frac{\partial u}{\partial \theta}\right) + \frac{1}{r^2 \sin^2\theta}\frac{\partial^2 u}{\partial \phi^2}.$$

### A.2.6 Pattern to remember
- The *Cartesian* forms are simplest because Cartesian basis vectors don't change direction.
- In *curvilinear* coordinates, the extra factors of $\rho$, $r$, $\sin\theta$ come from how distance and volume scale with angles.
- For PDEs with circular or spherical symmetry, choose the matching coordinate system — many terms drop out and the problem becomes much easier.

---

## A.3 Classifying PDEs

### A.3.1 The four classification questions

For any PDE, you should be able to answer these four questions:

1. **What is its order?**
2. **Is it linear or non-linear?**
3. **Is it homogeneous or inhomogeneous?**
4. **(For 2nd-order linear PDEs only)** Is it elliptic, parabolic, or hyperbolic?

### A.3.2 Order — how to count

The **order** is just the order of the highest derivative that appears.

Quick examples to internalise:

- $\frac{\partial u}{\partial t} = \left(\frac{\partial u}{\partial y}\right)^2 + \frac{\partial u}{\partial x}$ — first order. (The fact that one derivative is squared affects linearity, not order.)
- $\frac{\partial u}{\partial t} \cdot \frac{\partial u}{\partial x} = \left(\frac{\partial^2 u}{\partial y^2}\right)^3$ — second order. (Highest derivative is $u_{yy}$, regardless of the cube on it.)
- $\frac{\partial^2 u}{\partial t^2} = c^2 \frac{\partial^4 u}{\partial x^4}$ — fourth order.

**The rule:** find the highest-order derivative; the *exponent* on that derivative does *not* affect the order.

### A.3.3 Linearity — the test

A PDE is **linear** if and only if:

1. The dependent variable $u$ never multiplies itself or any of its derivatives.
2. No derivative is raised to a power other than 1.
3. $u$ never appears inside a non-linear function (no $\sin u$, $\sqrt{u}$, $e^u$, $u^2$, etc.).

If *any* of these fail, the PDE is non-linear.

Examples (worth committing to memory):

- $\frac{\partial u}{\partial x} + u = \frac{\partial u}{\partial y}$ — **linear**.
- $u\frac{\partial u}{\partial x} = \frac{\partial u}{\partial y}$ — **non-linear** (because $u$ multiplies a derivative of $u$).
- $\left(\frac{\partial u}{\partial x}\right)^2 + u = \frac{\partial u}{\partial y}$ — **non-linear** (a derivative is squared).
- $\frac{\partial u}{\partial x} + \sqrt{u} = \frac{\partial u}{\partial y}$ — **non-linear** (square root of $u$).

### A.3.4 Homogeneous vs inhomogeneous — the safe test

For **linear PDEs**, the clean definition is:

- **Homogeneous:** the equation can be written as $\mathcal L u = 0$.
- **Inhomogeneous:** the equation can be written as $\mathcal L u = f$, where $f$ is a known non-zero function or source term independent of $u$.

Examples:
- $u_t - g u_{xx} = 0$ is homogeneous.
- $u_t - g u_{xx} = L\sin y$ is inhomogeneous because the right-hand side is an external source independent of $u$.

For **nonlinear PDEs**, the word "homogeneous" is less universally used. A useful practical phrase is: "there is no independent forcing/source term". For example, $u_{xt}=\sinh u$ has no external source term, but because it is nonlinear, the ordinary linear homogeneous/inhomogeneous distinction should be used with care.

### A.3.5 The elliptic / parabolic / hyperbolic test

This applies *only* to second-order linear PDEs. Write the PDE in the standard form
$$A u_{xx} + B u_{xy} + C u_{yy} + (\text{lower-order terms}) = 0.$$
Compute the discriminant
$$\Delta = B^2 - 4AC.$$

- $\Delta < 0$: **elliptic** (e.g. Laplace's equation; describes equilibrium/steady-state).
- $\Delta = 0$: **parabolic** (e.g. heat equation; describes diffusion).
- $\Delta > 0$: **hyperbolic** (e.g. wave equation; describes wave propagation).

The names suggest the analogy with conic sections $Ax^2 + Bxy + Cy^2 = \text{const}$: ellipse if $\Delta<0$, parabola if $\Delta=0$, hyperbola if $\Delta>0$.

### A.3.6 Working through Problem Sheet 1, Question 3

We classify each given PDE step by step.

---

**(a)** $\dfrac{\partial u}{\partial t} + 2\kappa \dfrac{\partial u}{\partial x} - \dfrac{\partial^3 u}{\partial x^3} + 3u\dfrac{\partial u}{\partial x} = 2u\dfrac{\partial^2 u}{\partial x^2} + u\dfrac{\partial^3 u}{\partial t^3}$

**Order:** Look for the highest derivative. We see $\partial^3 u/\partial x^3$ and $\partial^3 u/\partial t^3$ — both third order. **Order = 3**.

**Linearity:** Scan each term:
- $u_t$ ✓ linear.
- $2\kappa u_x$ ✓ linear.
- $-u_{xxx}$ ✓ linear.
- $3u\, u_x$ — $u$ multiplies $u_x$. ✗ Non-linear.
- $2u\, u_{xx}$ — same problem. ✗ Non-linear.
- $u\, u_{ttt}$ — same. ✗ Non-linear.

So this PDE is **non-linear**.

**Homogeneity:** Every term contains $u$ or a derivative of $u$. **Homogeneous**.

**Type:** Not applicable. The elliptic/parabolic/hyperbolic classification is only for *2nd-order linear* PDEs. This is 3rd-order *and* non-linear.

---

**(b)** $\dfrac{\partial u}{\partial t} + H\dfrac{\partial^2 u}{\partial x^2} + u\dfrac{\partial u}{\partial x} = 0$

**Order:** Highest is $u_{xx}$. **Order = 2**.

**Linearity:** The $u\, u_x$ term has $u$ multiplying its derivative. **Non-linear** (specifically, this is called *quasi-linear* because the highest-order derivative still appears linearly — the non-linearity is only in the lower-order terms).

**Homogeneity:** Every term has $u$. **Homogeneous**.

**Type:** Strictly speaking the discriminant test is for fully linear equations, but we can identify the *principal part* (the highest-order derivatives only). Here, treating $(x, t)$ as our two coordinates with $A$ for $u_{xx}$, $B$ for $u_{xt}$, $C$ for $u_{tt}$:
- $A = H$ (coefficient of $u_{xx}$).
- $B = 0$ (no $u_{xt}$ term).
- $C = 0$ (no $u_{tt}$ term).

$\Delta = 0^2 - 4(H)(0) = 0$ → **parabolic**.

This makes physical sense: it looks like the heat equation $u_t = -H u_{xx}$ (with a non-linear advection term), and heat equations are parabolic.

---

**(c)** $7\dfrac{\partial^2 u}{\partial \rho^2} + 2\dfrac{\partial^2 u}{\partial \rho \partial \phi} + 6\dfrac{\partial^2 u}{\partial \phi^2} - 3\dfrac{\partial u}{\partial \rho} - 2\dfrac{\partial u}{\partial \phi} - 5u = 0$

**Order:** All highest derivatives are second order. **Order = 2**.

**Linearity:** No products of $u$ with itself or its derivatives, no powers of derivatives. **Linear**.

**Homogeneity:** Every term has $u$. **Homogeneous**.

**Type:** With independent variables $(\rho, \phi)$:
- $A = 7$ (coefficient of $u_{\rho\rho}$).
- $B = 2$ (coefficient of $u_{\rho\phi}$).
- $C = 6$ (coefficient of $u_{\phi\phi}$).

$\Delta = B^2 - 4AC = 4 - 4(7)(6) = 4 - 168 = -164$.

Since $\Delta < 0$, **elliptic**.

---

**(d)** $\dfrac{\partial^2 u}{\partial x \partial t} = \sinh u$

**Order:** $u_{xt}$ is second order. **Order = 2**.

**Linearity:** $\sinh u$ is a non-linear function of $u$. **Non-linear**.

**Homogeneity / source term:** This equation has no independent forcing term. However, because $\sinh u$ is nonlinear, it is better to say "unforced nonlinear PDE" rather than relying too strongly on the linear homogeneous/inhomogeneous terminology. The zero solution $u\equiv 0$ is still a solution.

**Type:** The discriminant test is technically for linear PDEs, but we can apply it to the principal part. With independent variables $(x, t)$:
- $A = 0$ (no $u_{xx}$ term).
- $B = 1$ (coefficient of $u_{xt}$).
- $C = 0$ (no $u_{tt}$ term).

$\Delta = 1^2 - 4(0)(0) = 1 > 0$ → **hyperbolic**.

---

**(e)** $9u + \dfrac{\partial u}{\partial x} + 9\dfrac{\partial^2 u}{\partial y^2} = 0$

**Order:** $u_{yy}$ is second order. **Order = 2**.

**Linearity:** All terms linear in $u$ and its derivatives. **Linear**.

**Homogeneity:** Every term contains $u$. **Homogeneous**.

**Type:** With $(x, y)$:
- $A = 0$ (no $u_{xx}$).
- $B = 0$.
- $C = 9$ (coefficient of $u_{yy}$).

$\Delta = 0 - 4(0)(9) = 0$ → **parabolic**.

---

**(f)** $\nabla^2 u = -\dfrac{\sigma}{\varepsilon_0}$ (Poisson's equation)

**Order:** Laplacian contains second derivatives. **Order = 2**.

**Linearity:** The Laplacian is a sum of second derivatives, all linear. **Linear**.

**Homogeneity:** The right-hand side $-\sigma/\varepsilon_0$ has no $u$ in it (assuming $\sigma$ is a known charge density independent of $u$). **Inhomogeneous**.

**Type:** The Laplacian's principal part has $A = 1$, $B = 0$, $C = 1$ (one for each spatial direction), giving $\Delta = 0 - 4 = -4 < 0$ → **elliptic**.

---

**(g)** $-8\dfrac{\partial^2 u}{\partial y^2} - 9\dfrac{\partial u}{\partial y} + 7\dfrac{\partial^2 u}{\partial x^2} - 3u + 7x + 2\dfrac{\partial u}{\partial x} = 0$

**Order:** Both $u_{xx}$ and $u_{yy}$ are second order. **Order = 2**.

**Linearity:** All terms linear in $u$ and its derivatives. **Linear**.

**Homogeneity:** The term $7x$ has no $u$. **Inhomogeneous**.

**Type:** With $(x, y)$:
- $A = 7$ (coefficient of $u_{xx}$).
- $B = 0$.
- $C = -8$ (coefficient of $u_{yy}$).

$\Delta = 0^2 - 4(7)(-8) = 0 + 224 = 224 > 0$ → **hyperbolic**.

### A.3.7 Pattern to remember

When you see a 2nd-order linear PDE, immediately reach for $A, B, C$ — the coefficients of $u_{xx}$, $u_{xy}$, and $u_{yy}$. Compute $B^2 - 4AC$. Sign tells you the family (elliptic/parabolic/hyperbolic) which strongly hints at:
- The expected solution methods.
- The boundary/initial conditions you'll need.
- The physical context (equilibrium / diffusion / wave propagation).

---

# Part B — Boundary Conditions and Solution Methods

## B.1 What we Need to Solve a PDE

### B.1.1 The big picture

To solve a PDE *uniquely*, the equation alone is never enough. We always need extra information that pins down our specific physical situation. Think of it this way: many different physical scenarios can satisfy the same PDE. The PDE describes the *physics*; the additional conditions describe the *specific situation*.

### B.1.2 The two types of extra information

1. **Initial conditions** — needed if there's a time dependence. They specify the state of the system across the whole spatial domain at the starting time.

2. **Boundary conditions** — needed always (if the spatial domain has boundaries). They specify what's happening at the *edges* of the spatial domain at all times.

### B.1.3 Initial conditions in detail

If the PDE is first-order in time (like the heat equation $u_t = \kappa \nabla^2 u$), we need *one* initial condition: typically $u(\mathbf{x}, 0) = f(\mathbf{x})$.

If the PDE is second-order in time (like the wave equation $u_{tt} = c^2 \nabla^2 u$), we need *two* initial conditions: typically $u(\mathbf{x}, 0)$ and $u_t(\mathbf{x}, 0)$ (initial position *and* initial velocity, if you think of it as a vibrating string).

Why? Because integrating an $n$-th order time derivative produces $n$ constants of integration, which need $n$ pieces of data to fix.

If there's *no* time dependence at all (a steady-state problem like Laplace's equation), no initial condition is needed.

### B.1.4 Boundary conditions in detail

There are several "types" depending on what is specified on the boundary. Imagine you're solving for the temperature in a metal plate. Along each edge of the plate, the question is: what do we know?

**Dirichlet (first-type):** the value of $u$ is specified on the boundary.
- Example: temperature held at exactly $50°\text{C}$ along an edge.
- Mathematically: $u(\mathbf{x}_{\text{boundary}}) = g(\mathbf{x})$.

**Neumann (second-type):** the *normal derivative* $\partial u/\partial n$ is specified on the boundary.
- Example: an insulated wall, where no heat flows through, so $\partial u/\partial n = 0$.
- The "normal derivative" means the derivative perpendicular to the boundary, pointing outward.

**Robin (third-type):** a linear combination of $u$ and $\partial u/\partial n$ is specified.
- Example: Newton's law of cooling — heat flux through a wall is proportional to the temperature difference between the wall and the ambient air. Mathematically: $\alpha u + \beta\, \partial u/\partial n = g$.

**Cauchy:** *both* $u$ and $\partial u/\partial n$ are specified on the boundary or initial surface.
- Example: a vibrating string — at $t=0$, we specify both the initial displacement and the initial velocity.

**Mixed:** different parts of the boundary have different types of conditions.

### B.1.5 Homogeneous vs inhomogeneous boundary conditions

A boundary condition is **homogeneous** if the prescribed value or derivative is *zero*, e.g. $u = 0$ on the boundary, or $\partial u/\partial n = 0$.

It is **inhomogeneous** if it is a non-zero constant or function, e.g. $u = 50°\text{C}$ on the boundary.

This distinction matters because separation of variables works most cleanly when boundary conditions are homogeneous. If they aren't, you often have to use a clever trick like splitting the solution into a steady-state part plus a transient part (we'll see this in the heat-bath rod problem).

---

## B.2 When Can We Solve a PDE Exactly?

### B.2.1 Problem (Sheet 1, Q5)
Outline under what circumstances an exact solution to a PDE is possible, and when a numerical approximation must be used instead.

### B.2.2 Conditions favouring an exact solution

For an analytical (closed-form) solution to exist, *all* of the following typically need to hold:

- **The PDE is linear.** Non-linear PDEs almost never admit closed-form solutions in general (Navier–Stokes is the famous example).

- **Coefficients are constant.** If properties (like thermal conductivity $\kappa$) vary in space or time, the methods break down.

- **The geometry is regular.** Rectangles, disks, cylinders, spheres — anything aligned with a standard coordinate system. Irregular shapes (a wing, a bone) prevent clean separation of variables.

- **Boundary/initial conditions are simple.** Typically homogeneous, or expressible as functions amenable to Fourier series, integral transforms, or recognisable special functions.

### B.2.3 When numerical methods are required

In real-world applied science, exact solutions are rare. Numerical methods (finite difference, finite element, finite volume) are needed when:

- The PDE is **non-linear** (turbulence, plasticity, large-amplitude waves).
- The geometry is **irregular** (an aircraft wing, biological tissue).
- The material has **variable coefficients** (composite materials, layered earth in seismic problems).
- Boundary/initial data is **complex or experimental** (e.g. measured weather data driving a climate simulation).

### B.2.4 The principle of superposition (the crucial enabler)

For a *linear* PDE $\mathcal{L}u = 0$, if $u_1$ and $u_2$ are both solutions, so is $au_1 + bu_2$ for any constants $a, b$. This works because:
$$\mathcal{L}(au_1 + bu_2) = a\,\mathcal{L}u_1 + b\,\mathcal{L}u_2 = a(0) + b(0) = 0.$$

The implication is enormous: we can build the answer to a complicated boundary-value problem by adding together many simpler solutions. This is exactly what we do in:
- **Fourier series** — adding sinusoidal eigenfunctions.
- **Eigenfunction expansions** — adding solutions of the homogeneous problem.
- **Green's function method** — integrating responses to point sources.

For *non-linear* PDEs, superposition fails, which is why they're so much harder.

---

# Part C — Solution by Inspection (Sheet 1, Q6)

## C.1 The strategy

We're given a function $u$ and asked: which standard PDE does it solve (if any)?

The three test PDEs are:

- **Laplace (2D):** $u_{xx} + u_{yy} = 0$.
- **Diffusion (1D):** $u_t = D\, u_{xx}$ for some constant $D$.
- **Wave (1D):** $u_{tt} = c^2\, u_{xx}$ for some constant wave speed $c$.

**Strategy:**
1. Identify which independent variables $u$ depends on. If $(x, y)$, test Laplace. If $(x, t)$, test diffusion and wave.
2. Compute the relevant partial derivatives.
3. Substitute into the test equation and check.

We'll work through each part of Sheet 1 Q6.

---

## C.2 Part (a): $u = e^{kx}\sin(ky)$

**What variables?** $x$ and $y$. → Test against **Laplace's equation**.

**Compute $u_x$ and $u_{xx}$.** Treat $y$ (and hence $\sin(ky)$) as a constant when differentiating with respect to $x$:
$$u_x = \frac{\partial}{\partial x}\!\left[e^{kx}\sin(ky)\right] = k\,e^{kx}\sin(ky).$$
$$u_{xx} = \frac{\partial}{\partial x}\!\left[k\,e^{kx}\sin(ky)\right] = k^2\,e^{kx}\sin(ky).$$

**Compute $u_y$ and $u_{yy}$.** Treat $e^{kx}$ as a constant when differentiating with respect to $y$:
$$u_y = \frac{\partial}{\partial y}\!\left[e^{kx}\sin(ky)\right] = k\,e^{kx}\cos(ky).$$
$$u_{yy} = \frac{\partial}{\partial y}\!\left[k\,e^{kx}\cos(ky)\right] = -k^2\,e^{kx}\sin(ky).$$

**Add:**
$$u_{xx} + u_{yy} = k^2 e^{kx}\sin(ky) - k^2 e^{kx}\sin(ky) = 0. \;\checkmark$$

**Conclusion:** $u$ is a **solution of Laplace's equation**.

---

## C.3 Part (b): $u = \dfrac{a}{\sqrt{t}}\, e^{-bx^2/t}$

**What variables?** $x$ and $t$. → Test against **diffusion** (and wave).

This one is messy, so we go slowly.

**Compute $u_t$.** We have $u = a\,t^{-1/2}\, e^{-bx^2/t}$, a product of two factors that both depend on $t$. Use the product rule:
$$u_t = \underbrace{a\frac{d}{dt}(t^{-1/2})}_{\text{first factor}}\cdot e^{-bx^2/t} + a\,t^{-1/2}\cdot \underbrace{\frac{\partial}{\partial t}\!\left(e^{-bx^2/t}\right)}_{\text{second factor}}.$$

For the first factor: $\frac{d}{dt}(t^{-1/2}) = -\tfrac{1}{2} t^{-3/2}$.

For the second factor (chain rule): the inner function is $-bx^2/t = -bx^2 t^{-1}$, whose derivative with respect to $t$ is $bx^2 t^{-2} = bx^2/t^2$. So
$$\frac{\partial}{\partial t}\!\left(e^{-bx^2/t}\right) = e^{-bx^2/t}\cdot \frac{bx^2}{t^2}.$$

Putting it together:
$$u_t = -\frac{a}{2}\,t^{-3/2}\,e^{-bx^2/t} + a\,t^{-1/2}\,e^{-bx^2/t}\,\frac{bx^2}{t^2}.$$

Factor out $a\,t^{-3/2}\,e^{-bx^2/t}$:
$$u_t = \frac{a}{t^{3/2}}e^{-bx^2/t}\!\left(-\frac{1}{2} + \frac{bx^2}{t}\right) = \frac{a}{t^{3/2}}e^{-bx^2/t}\!\left(\frac{bx^2}{t} - \frac{1}{2}\right). \quad (\star)$$

**Compute $u_x$.** Now $t$ is held constant. The exponent $-bx^2/t$ has derivative $-2bx/t$ with respect to $x$:
$$u_x = \frac{a}{\sqrt{t}}\,e^{-bx^2/t}\,\left(-\frac{2bx}{t}\right) = -\frac{2abx}{t^{3/2}}\,e^{-bx^2/t}.$$

**Compute $u_{xx}$.** This is the derivative of a product; let $P(x) = -2abx/t^{3/2}$ and $Q(x) = e^{-bx^2/t}$:
$$u_{xx} = P'(x) Q(x) + P(x) Q'(x).$$
- $P'(x) = -2ab/t^{3/2}$.
- $Q'(x) = e^{-bx^2/t}\cdot(-2bx/t)$.

So
$$u_{xx} = -\frac{2ab}{t^{3/2}}\,e^{-bx^2/t} + \left(-\frac{2abx}{t^{3/2}}\right)\!\left(-\frac{2bx}{t}\right)e^{-bx^2/t}$$
$$= -\frac{2ab}{t^{3/2}}\,e^{-bx^2/t} + \frac{4ab^2 x^2}{t^{5/2}}\,e^{-bx^2/t}.$$

Factor out $-\frac{2ab}{t^{3/2}}\,e^{-bx^2/t}$ (taking care with signs):
$$u_{xx} = -\frac{2ab}{t^{3/2}}\,e^{-bx^2/t}\!\left(1 - \frac{2bx^2}{t}\right) = \frac{2ab}{t^{3/2}}\,e^{-bx^2/t}\!\left(\frac{2bx^2}{t} - 1\right).$$

Now divide by 2:
$$u_{xx} = \frac{4ab}{t^{3/2}}\,e^{-bx^2/t}\!\left(\frac{bx^2}{t} - \frac{1}{2}\right). \quad (\star\star)$$

**Compare $(\star)$ and $(\star\star)$.** They have the same shape — both are
$$\frac{a}{t^{3/2}}e^{-bx^2/t}\!\left(\frac{bx^2}{t} - \frac{1}{2}\right)$$
times a constant: $u_t$ has prefactor 1, while $u_{xx}$ has prefactor $4b$.

Therefore:
$$u_{xx} = 4b\, u_t \;\Longleftrightarrow\; u_t = \frac{1}{4b}\, u_{xx}. \;\checkmark$$

**Conclusion:** This is a **solution of the diffusion equation** with $D = 1/(4b)$.

(Aside: this is in fact the **fundamental solution** of the 1D diffusion equation — the Green's function describing how an initial point concentration spreads as a Gaussian over time.)

---

## C.4 Part (c): $u = \ln(x^2 + y^2)$

**What variables?** $x$ and $y$. → Test against **Laplace**.

**Compute $u_x$.** Chain rule with inner function $x^2 + y^2$:
$$u_x = \frac{1}{x^2 + y^2}\cdot 2x = \frac{2x}{x^2 + y^2}.$$

**Compute $u_{xx}$ via the quotient rule.** Let $N = 2x$, $D = x^2+y^2$. Then
$$\left(\frac{N}{D}\right)' = \frac{N' D - N D'}{D^2} = \frac{2(x^2+y^2) - 2x(2x)}{(x^2+y^2)^2} = \frac{2x^2 + 2y^2 - 4x^2}{(x^2+y^2)^2} = \frac{2y^2 - 2x^2}{(x^2+y^2)^2}.$$

**Compute $u_{yy}$ by symmetry.** The function is symmetric under $x \leftrightarrow y$, so swapping in the formula above:
$$u_{yy} = \frac{2x^2 - 2y^2}{(x^2+y^2)^2}.$$

**Add:**
$$u_{xx} + u_{yy} = \frac{(2y^2 - 2x^2) + (2x^2 - 2y^2)}{(x^2+y^2)^2} = \frac{0}{(x^2+y^2)^2} = 0. \;\checkmark$$

**Conclusion:** **Solution of Laplace's equation away from the origin.** The calculation is valid wherever $(x,y)\neq(0,0)$. At $(0,0)$ the function is singular, so the domain must exclude the origin. Physically, this is the 2D analogue of the Coulomb potential — the potential of an infinite line of charge.

---

## C.5 Part (d): $u = e^{-iat}\sin(bx)$

**What variables?** $x$ and $t$. → Test against wave and diffusion.

**Time derivatives.**
$$u_t = \frac{d}{dt}(e^{-iat})\cdot \sin(bx) = -ia\,e^{-iat}\sin(bx) = -ia\, u.$$
$$u_{tt} = \frac{d}{dt}(-ia\,e^{-iat})\cdot \sin(bx) = (-ia)^2\, e^{-iat}\sin(bx) = -a^2\, u.$$

**Spatial derivatives.**
$$u_x = e^{-iat}\,b\cos(bx).$$
$$u_{xx} = e^{-iat}\,(-b^2)\sin(bx) = -b^2\, u.$$

**Compare:** $u_{tt} = -a^2 u$ and $u_{xx} = -b^2 u$. So
$$u_{tt} = \frac{a^2}{b^2}\,u_{xx} = \left(\frac{a}{b}\right)^2 u_{xx}. \;\checkmark$$

This matches the wave equation $u_{tt} = c^2 u_{xx}$ with **$c = a/b$**.

(Does it satisfy the diffusion equation? We'd need $u_t = D u_{xx}$, i.e. $-ia\,u = D(-b^2 u) = -Db^2\,u$. This requires $ia = Db^2$, but $D$ should be real. So no — it's not a diffusion solution.)

**Conclusion:** **Solution of the wave equation.**

---

## C.6 Part (e): $u = \sin(x - vt)$

**What variables?** $x$ and $t$. → Test wave/diffusion.

**Time derivatives.** With chain rule (inner function $x - vt$, derivative $-v$ w.r.t. $t$):
$$u_t = \cos(x-vt)\cdot(-v) = -v\cos(x-vt).$$
$$u_{tt} = -v\cdot[-\sin(x-vt)]\cdot(-v) = -v^2\sin(x-vt).$$

**Spatial derivatives.** Inner function derivative $+1$ w.r.t. $x$:
$$u_x = \cos(x-vt).$$
$$u_{xx} = -\sin(x-vt).$$

**Compare:** $u_{tt} = -v^2\sin(x-vt) = v^2\cdot[-\sin(x-vt)] = v^2\, u_{xx}$. ✓

**Conclusion:** **Solution of the wave equation** with speed $v$.

This is a special case of d'Alembert's general solution $f(x-vt) + g(x+vt)$: any twice-differentiable function of $x - vt$ alone is a right-travelling wave at speed $v$.

---

## C.7 Part (f): $u = \ln(xy) = \ln x + \ln y$

**What variables?** $x$ and $y$. → Test Laplace.

(The trick of writing $\ln(xy) = \ln x + \ln y$ separates the variables — much easier to differentiate.)

$$u_x = \frac{1}{x}, \qquad u_{xx} = -\frac{1}{x^2}.$$
$$u_y = \frac{1}{y}, \qquad u_{yy} = -\frac{1}{y^2}.$$

$$u_{xx} + u_{yy} = -\frac{1}{x^2} - \frac{1}{y^2} \neq 0 \;\;(\text{except in the limit}).$$

**Conclusion:** **None of the three.** It's not Laplace. It can't be a wave/diffusion solution either, because it has no $t$ dependence (so its time derivatives are zero, which would force $u_{xx} = 0$, which it doesn't satisfy).

---

## C.8 Part (g): $u = e^{x - vt}$

$$u_t = e^{x-vt}\cdot(-v) = -v\,u.$$
$$u_{tt} = (-v)^2\, u = v^2\, u.$$
$$u_x = u, \qquad u_{xx} = u.$$

So $u_{tt} = v^2 u = v^2 u_{xx}$. ✓

**Conclusion:** **Solution of the wave equation** with speed $v$ (a right-travelling exponential pulse).

---

## C.9 The pattern across all of C

Some general lessons:

- Functions of the form $f(x \pm vt)$ for any twice-differentiable $f$ are wave-equation solutions. (D'Alembert's theorem made manifest.)

- Functions of the form $\frac{1}{\sqrt{t}}e^{-x^2/(4Dt)}$ are diffusion-equation solutions (the Gaussian heat kernel).

- Functions that are the real or imaginary part of an analytic function $F(x+iy)$ — like $\ln(x^2+y^2) = 2\,\text{Re}(\ln(x+iy))$ — are Laplace solutions. These are called **harmonic functions**.

- Just because a function involves multiple variables doesn't mean it solves a known PDE — sometimes the answer is "none of them" (like part f).

---

# Part D — D'Alembert's Solution of the Wave Equation (Sheet 1, Q7)

## D.1 What we're trying to do

We want to find the **general solution** to the 1D wave equation
$$\frac{\partial^2 u}{\partial t^2} = v^2 \frac{\partial^2 u}{\partial x^2}.$$
The strategy is to use a clever **change of variables** that simplifies the PDE so much that we can solve it by direct integration.

## D.2 Setting up the change of variables

Define new coordinates:
$$p = x + vt, \qquad q = x - vt.$$
These are called **characteristic coordinates**. $p = \text{const.}$ and $q = \text{const.}$ are the two families of "characteristic lines" along which information propagates in the wave equation. We now express the wave equation in terms of $p$ and $q$ instead of $x$ and $t$.

## D.3 Computing first derivatives via the chain rule

The chain rule for a function of two variables says:
$$\frac{\partial u}{\partial x} = \frac{\partial u}{\partial p}\frac{\partial p}{\partial x} + \frac{\partial u}{\partial q}\frac{\partial q}{\partial x}.$$

Here we just need to know how $p$ and $q$ depend on $x$ and $t$:
- $\dfrac{\partial p}{\partial x} = \dfrac{\partial}{\partial x}(x + vt) = 1$ (treating $t$ as fixed).
- $\dfrac{\partial q}{\partial x} = \dfrac{\partial}{\partial x}(x - vt) = 1$.
- $\dfrac{\partial p}{\partial t} = \dfrac{\partial}{\partial t}(x + vt) = v$.
- $\dfrac{\partial q}{\partial t} = \dfrac{\partial}{\partial t}(x - vt) = -v$.

So:
$$\frac{\partial u}{\partial x} = \frac{\partial u}{\partial p}\cdot 1 + \frac{\partial u}{\partial q}\cdot 1 = \frac{\partial u}{\partial p} + \frac{\partial u}{\partial q}. \quad (1)$$
$$\frac{\partial u}{\partial t} = \frac{\partial u}{\partial p}\cdot v + \frac{\partial u}{\partial q}\cdot(-v) = v\!\left(\frac{\partial u}{\partial p} - \frac{\partial u}{\partial q}\right). \quad (2)$$

It's useful to think of these as **operator identities** acting on any function:
$$\frac{\partial}{\partial x} = \frac{\partial}{\partial p} + \frac{\partial}{\partial q}, \qquad \frac{\partial}{\partial t} = v\!\left(\frac{\partial}{\partial p} - \frac{\partial}{\partial q}\right).$$

## D.4 Computing the second derivatives

We apply the operators to themselves.

**Compute $u_{xx}$:**
$$\frac{\partial^2 u}{\partial x^2} = \frac{\partial}{\partial x}\!\left(\frac{\partial u}{\partial x}\right) = \left(\frac{\partial}{\partial p} + \frac{\partial}{\partial q}\right)\!\left(\frac{\partial u}{\partial p} + \frac{\partial u}{\partial q}\right).$$

Distributing (treating it like multiplying two binomials):
$$= \frac{\partial^2 u}{\partial p^2} + \frac{\partial^2 u}{\partial p\,\partial q} + \frac{\partial^2 u}{\partial q\,\partial p} + \frac{\partial^2 u}{\partial q^2}.$$

Assuming $u$ is smooth enough that mixed partials commute ($u_{pq} = u_{qp}$):
$$u_{xx} = u_{pp} + 2u_{pq} + u_{qq}. \quad (3)$$

**Compute $u_{tt}$:**
$$u_{tt} = v\!\left(\frac{\partial}{\partial p} - \frac{\partial}{\partial q}\right)\!\left[v\!\left(\frac{\partial u}{\partial p} - \frac{\partial u}{\partial q}\right)\right] = v^2\!\left(\frac{\partial}{\partial p} - \frac{\partial}{\partial q}\right)\!\left(u_p - u_q\right).$$

Distributing:
$$= v^2\bigl(u_{pp} - u_{pq} - u_{qp} + u_{qq}\bigr) = v^2(u_{pp} - 2u_{pq} + u_{qq}). \quad (4)$$

## D.5 Substituting into the wave equation

Plug $(3)$ and $(4)$ into $u_{tt} = v^2 u_{xx}$:
$$v^2(u_{pp} - 2u_{pq} + u_{qq}) = v^2(u_{pp} + 2u_{pq} + u_{qq}).$$

Divide both sides by $v^2$ (which is non-zero, since the wave is propagating):
$$u_{pp} - 2u_{pq} + u_{qq} = u_{pp} + 2u_{pq} + u_{qq}.$$

Subtract $u_{pp} + u_{qq}$ from both sides:
$$-2u_{pq} = 2u_{pq}.$$

Move everything to one side:
$$-4u_{pq} = 0 \;\Longrightarrow\; \boxed{\frac{\partial^2 u}{\partial p\, \partial q} = 0.}$$

This is the desired simplified form. The wave equation, in characteristic coordinates, says that the mixed partial derivative is zero — much easier to solve.

## D.6 Solving the simplified equation

Rewrite as
$$\frac{\partial}{\partial p}\!\left(\frac{\partial u}{\partial q}\right) = 0.$$

This says: the function $\partial u/\partial q$, viewed as a function of $p$ (with $q$ fixed), has zero derivative. So $\partial u/\partial q$ doesn't depend on $p$ at all — it is some function of $q$ alone:
$$\frac{\partial u}{\partial q} = h(q),$$
where $h$ is an arbitrary differentiable function.

Now integrate with respect to $q$ (treating $p$ as a constant):
$$u(p, q) = \int h(q)\,dq + (\text{constant of integration with respect to }q).$$

Crucially, the "constant of integration" can be *any function of $p$*, since differentiating it with respect to $q$ gives zero. Call this arbitrary function $F(p)$. And let $G(q) := \int h(q)\,dq$ be an antiderivative of $h$ (also an arbitrary differentiable function, since $h$ was arbitrary). Then:
$$u(p, q) = F(p) + G(q).$$

## D.7 Returning to original variables

Substitute back $p = x + vt$ and $q = x - vt$:
$$u(x, t) = F(x + vt) + G(x - vt).$$

Since $F$ and $G$ are arbitrary differentiable functions, we can rename them however we want. The standard form (matching the question) is:
$$\boxed{u(x, t) = f(x - vt) + g(x + vt).}$$

This is **D'Alembert's general solution** to the 1D wave equation.

## D.8 Physical interpretation

- The function $f(x - vt)$ has its argument shifted by $vt$ as $t$ increases. So the graph of $f$ as a function of $x$ moves bodily to the right with speed $v$, *without changing shape*. This is a **right-travelling wave**.

- Similarly, $g(x + vt)$ moves to the left at speed $v$ — a **left-travelling wave**.

- The general solution is a superposition of these two. Any specific physical situation (initial displacement, initial velocity, fixed ends, etc.) determines what the specific functions $f$ and $g$ are.

## D.9 Pattern to remember

When you see $u_{tt} = v^2 u_{xx}$ on an *infinite* domain, the answer always has the structure $f(x-vt) + g(x+vt)$. The boundary/initial conditions then determine $f$ and $g$. We'll see in Section J.5 how to evaluate these for the three standard kinds of initial conditions (Dirichlet, Neumann, Cauchy).

---

# Part E — Separation of Variables: Laplace's Equation

This is the central technique of the course. We work through it very slowly the first time.

## E.1 The 9-step recipe (illustrated on a semi-infinite plate)

We solve the lecture example to establish the method, then we'll re-use it on Sheet 1 Q8, Q9, Q10.

### E.1.1 The problem

Find the steady-state temperature $u(x, y)$ in a semi-infinite plate ($0 \le x \le 10$, $0 \le y < \infty$) with boundary conditions:
- $u(0, y) = 0$ (left edge cold)
- $u(10, y) = 0$ (right edge cold)
- $u(x, \infty) = 0$ (vanishes at infinity)
- $u(x, 0) = 100$ (bottom edge hot)

### E.1.2 Step 1 — State the problem

We want $u(x, y)$ in the plate. Steady state → no time dependence → no initial condition needed. We have four boundary conditions and we expect them to be enough.

### E.1.3 Step 2 — Choose the PDE

Steady-state heat conduction in 2D with no sources is governed by **Laplace's equation**:
$$\frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2} = 0.$$

### E.1.4 Step 3 — Try a separated form

The key assumption: the solution can be written as a product of a function of $x$ alone and a function of $y$ alone:
$$u(x, y) = X(x)\, Y(y).$$

This is a *guess* (technically called an *ansatz*). The justification is that *if* it works, it gives us a solution; combined with the principle of superposition, we can build up the general answer from many such products.

Substitute into Laplace's equation. Note:
- $\partial^2 u/\partial x^2 = X''(x)\,Y(y)$ (since $Y$ doesn't depend on $x$).
- $\partial^2 u/\partial y^2 = X(x)\,Y''(y)$.

So:
$$X''(x)\,Y(y) + X(x)\,Y''(y) = 0.$$

**Now divide both sides by $X(x)\,Y(y)$** (assuming neither is zero in the interior):
$$\frac{X''(x)}{X(x)} + \frac{Y''(y)}{Y(y)} = 0,$$
which we rearrange as:
$$\frac{X''(x)}{X(x)} = -\frac{Y''(y)}{Y(y)}.$$

### E.1.5 The "separation" insight

Look at this equation. The left side depends only on $x$, the right side only on $y$. But the equation must hold for *all* $(x, y)$ in the plate. The only way this is possible is if both sides are equal to the *same constant*.

Why? Suppose I fix $y$ and vary $x$. The right side is fixed (doesn't depend on $x$), but the left side could vary. The only way for the equation to hold across all $x$ is for the left side to be a constant. By symmetry, the right side is also constant, and they're equal.

Call this constant $-k^2$:
$$\frac{X''}{X} = -k^2, \qquad \frac{Y''}{Y} = k^2.$$

**Why $-k^2$?** The choice of sign is dictated by the boundary conditions we'll encounter. When the *bounded* spatial direction (here $x$, which goes from 0 to 10) has homogeneous boundary conditions, we want oscillatory (sinusoidal) solutions in that direction. Sines and cosines come from $X'' = -k^2 X$ (negative coefficient → oscillatory). Exponentials come from $Y'' = +k^2 Y$ (positive coefficient → exponential).

If we had chosen $+k^2$ for the $X$ equation instead, we'd get exponentials in $x$, which can't satisfy $X(0) = X(10) = 0$ except for the trivial solution. So the sign is chosen by foresight; if we'd chosen wrong, we'd find out very quickly and switch.

### E.1.6 Step 4 — The two ODEs

We now have:
$$X'' + k^2 X = 0, \qquad Y'' - k^2 Y = 0.$$

These are familiar second-order ODEs.

### E.1.7 Step 5 — Solve the ODEs

**For $X'' + k^2 X = 0$**: The general solution is
$$X(x) = A\cos(kx) + B\sin(kx),$$
where $A, B$ are constants.

**For $Y'' - k^2 Y = 0$**: The general solution is
$$Y(y) = C e^{ky} + D e^{-ky},$$
where $C, D$ are constants.

The full separated solution is:
$$u(x, y) = X(x)Y(y) = \bigl[A\cos(kx) + B\sin(kx)\bigr]\bigl[Ce^{ky} + De^{-ky}\bigr].$$

We have **four constants** ($A, B, C, D$) and **four boundary conditions**. This is the right balance — we expect a unique solution.

### E.1.8 Step 6 — Apply the boundary conditions, one at a time

**Boundary condition 1: $u(0, y) = 0$.**

Substitute $x = 0$:
$$u(0, y) = \bigl[A\cos(0) + B\sin(0)\bigr]\bigl[Ce^{ky} + De^{-ky}\bigr] = A \cdot \bigl[Ce^{ky} + De^{-ky}\bigr].$$
For this to equal zero *for all $y$*, we need $A = 0$ (we don't want the bracket to vanish, since that would force $C = D = 0$ and give us nothing).

Solution so far:
$$u(x, y) = B\sin(kx)\bigl[Ce^{ky} + De^{-ky}\bigr].$$

**Boundary condition 2: $u(10, y) = 0$.**

Substitute $x = 10$:
$$u(10, y) = B\sin(10k)\bigl[Ce^{ky} + De^{-ky}\bigr] = 0 \;\text{for all }y.$$

Setting $B = 0$ would kill the entire solution (trivial). So we need $\sin(10k) = 0$. This means
$$10k = n\pi \;\Longrightarrow\; k = \frac{n\pi}{10}, \qquad n = 1, 2, 3, \ldots$$

Note: $n = 0$ would give $k = 0$, hence $X = B \sin(0) = 0$, i.e. trivial. Negative integers give the same solutions as positive ones (because $\sin(-x) = -\sin(x)$ which we absorb into $B$). So we take $n = 1, 2, 3, \ldots$.

This is a quantisation effect: not all values of $k$ are allowed; only a discrete set called the **eigenvalues**.

The solution is now indexed by $n$:
$$u_n(x, y) = B_n \sin\!\left(\frac{n\pi x}{10}\right)\bigl[C_n e^{n\pi y/10} + D_n e^{-n\pi y/10}\bigr].$$

**Boundary condition 3: $u(x, \infty) = 0$.**

As $y \to \infty$, the term $e^{n\pi y/10}$ blows up, while $e^{-n\pi y/10}$ decays. For the solution to remain bounded (and indeed go to 0 at infinity), the coefficient of the growing exponential must vanish: $C_n = 0$.

Solution so far:
$$u_n(x, y) = B_n D_n \sin\!\left(\frac{n\pi x}{10}\right) e^{-n\pi y/10}.$$

The product $B_n D_n$ is just one constant; rename it $b_n$:
$$u_n(x, y) = b_n \sin\!\left(\frac{n\pi x}{10}\right) e^{-n\pi y/10}.$$

**Boundary condition 4: $u(x, 0) = 100$.**

Substitute $y = 0$:
$$u_n(x, 0) = b_n \sin\!\left(\frac{n\pi x}{10}\right) \cdot 1 = b_n\sin\!\left(\frac{n\pi x}{10}\right).$$

For this to equal $100$ (a constant) is impossible with a single $n$, since $\sin$ is not constant.

The fix: **superposition**. Linear combinations of solutions are solutions. So the most general solution we can build is
$$u(x, y) = \sum_{n=1}^{\infty} b_n \sin\!\left(\frac{n\pi x}{10}\right) e^{-n\pi y/10}.$$

### E.1.9 Step 7 — Build the Fourier series

At $y = 0$:
$$u(x, 0) = \sum_{n=1}^\infty b_n \sin\!\left(\frac{n\pi x}{10}\right) = 100.$$

This is a **Fourier sine series** for the function $f(x) = 100$ on the interval $[0, 10]$. The coefficients $b_n$ are determined by the standard Fourier formula.

### E.1.10 Step 8 — Compute the Fourier coefficients

The formula for the Fourier sine series of a function $f(x)$ on $[0, L]$ is:
$$b_n = \frac{2}{L}\int_0^L f(x)\sin\!\left(\frac{n\pi x}{L}\right) dx.$$

Here $L = 10$ and $f(x) = 100$:
$$b_n = \frac{2}{10}\int_0^{10} 100\sin\!\left(\frac{n\pi x}{10}\right) dx = 20\int_0^{10} \sin\!\left(\frac{n\pi x}{10}\right)dx.$$

Compute the integral:
$$\int_0^{10}\sin\!\left(\frac{n\pi x}{10}\right)dx = \left[-\frac{10}{n\pi}\cos\!\left(\frac{n\pi x}{10}\right)\right]_0^{10} = -\frac{10}{n\pi}\bigl[\cos(n\pi) - \cos(0)\bigr] = -\frac{10}{n\pi}\bigl[(-1)^n - 1\bigr].$$

Therefore:
$$b_n = 20 \cdot \left(-\frac{10}{n\pi}\right)\bigl[(-1)^n - 1\bigr] = -\frac{200}{n\pi}\bigl[(-1)^n - 1\bigr] = \frac{200}{n\pi}\bigl[1 - (-1)^n\bigr].$$

Now case-split on parity of $n$:
- **$n$ even:** $(-1)^n = 1$, so $1 - 1 = 0$, hence $b_n = 0$.
- **$n$ odd:** $(-1)^n = -1$, so $1 - (-1) = 2$, hence $b_n = \dfrac{400}{n\pi}$.

### E.1.11 Step 9 — Final solution

Plug coefficients back:
$$\boxed{u(x, y) = \frac{400}{\pi}\sum_{n\,\text{odd}}\frac{1}{n}\, \sin\!\left(\frac{n\pi x}{10}\right) e^{-n\pi y/10}.}$$

### E.1.12 Sanity checks

- At $x = 0$: every $\sin(0)$ vanishes, so $u(0, y) = 0$. ✓
- At $x = 10$: every $\sin(n\pi)$ vanishes, so $u(10, y) = 0$. ✓
- As $y \to \infty$: every exponential decays to 0, so $u(x, \infty) = 0$. ✓
- At $y = 0$: this is harder to check by hand, but trying e.g. $x = 5$ gives the series $\dfrac{400}{\pi}(1 - \tfrac13 + \tfrac15 - \tfrac17 + \cdots)$, and the alternating series $1 - 1/3 + 1/5 - \cdots = \pi/4$ (Leibniz's formula), so the result is $\dfrac{400}{\pi}\cdot\dfrac{\pi}{4} = 100$. ✓

---

## E.2 Sheet 1 Q8: Capped 10 cm × 20 cm copper sheet

### E.2.1 The problem

A uniform copper sheet of width 10 cm and length 20 cm has its bottom edge held at $50°\text{C}$ and the other three edges at $0°\text{C}$. Find the steady-state temperature $u(x, y)$ inside.

### E.2.2 Differences from the previous example

This problem is similar to the lecture-note semi-infinite plate but with one important difference: **the plate is finite in $y$** (it's capped at $y = 20$). This means we cannot discard the growing exponential in $y$ — both exponentials are valid in the bounded domain.

### E.2.3 Step 1 — Conditions

- $u(0, y) = 0$ (left edge).
- $u(10, y) = 0$ (right edge).
- $u(x, 20) = 0$ (top edge — the cap).
- $u(x, 0) = 50$ (bottom edge).

### E.2.4 Step 2 — Laplace's equation

$$u_{xx} + u_{yy} = 0.$$

### E.2.5 Steps 3–5 — Separation of variables

Same as before: let $u = X(x)Y(y)$. We get
$$X'' + k^2 X = 0, \qquad Y'' - k^2 Y = 0,$$
with general solution
$$u(x, y) = (A\cos kx + B\sin kx)(Ce^{ky} + De^{-ky}).$$

### E.2.6 Step 6 — Apply the homogeneous boundary conditions

**$u(0, y) = 0$:** As before, $A = 0$.
**$u(10, y) = 0$:** As before, $\sin(10k) = 0 \Rightarrow k = n\pi/10$, $n = 1, 2, 3, \ldots$.

So the eigenfunctions become:
$$u_n(x, y) = B_n\sin\!\left(\frac{n\pi x}{10}\right)\bigl[C_n e^{n\pi y/10} + D_n e^{-n\pi y/10}\bigr].$$

### E.2.7 The new step — Apply $u(x, 20) = 0$

Substitute $y = 20$:
$$u_n(x, 20) = B_n\sin\!\left(\frac{n\pi x}{10}\right)\bigl[C_n e^{2n\pi} + D_n e^{-2n\pi}\bigr] = 0.$$

For this to hold for all $x \in [0, 10]$, we need
$$C_n e^{2n\pi} + D_n e^{-2n\pi} = 0 \;\Longrightarrow\; C_n = -D_n e^{-4n\pi}. \quad (*)$$

This determines the *ratio* $C_n / D_n$ but not their individual values — that's good. We have one less unknown. The convention (per the problem sheet hint) is to set $D_n = 1$ and use $(*)$ to get $C_n = -e^{-4n\pi}$, but more flexibly we just keep $D_n$ as a free parameter.

Substitute back into the eigenfunction:
$$u_n(x, y) = B_n\sin\!\left(\frac{n\pi x}{10}\right)\bigl[-D_n e^{-4n\pi}e^{n\pi y/10} + D_n e^{-n\pi y/10}\bigr]$$
$$= B_n D_n\sin\!\left(\frac{n\pi x}{10}\right)\bigl[e^{-n\pi y/10} - e^{n\pi y/10 - 4n\pi}\bigr].$$

The product $B_n D_n$ is one combined constant; rename it $b_n$:
$$u_n(x, y) = b_n\sin\!\left(\frac{n\pi x}{10}\right)\bigl[e^{-n\pi y/10} - e^{n\pi y/10 - 4n\pi}\bigr].$$

### E.2.8 Step 7 — Superpose

The general solution is
$$u(x, y) = \sum_{n=1}^\infty b_n\sin\!\left(\frac{n\pi x}{10}\right)\bigl[e^{-n\pi y/10} - e^{n\pi y/10 - 4n\pi}\bigr].$$

### E.2.9 Step 8 — Apply the bottom-edge condition

At $y = 0$:
$$u(x, 0) = \sum_{n=1}^\infty b_n\sin\!\left(\frac{n\pi x}{10}\right)\bigl[e^{0} - e^{0 - 4n\pi}\bigr] = \sum_{n=1}^\infty b_n(1 - e^{-4n\pi})\sin\!\left(\frac{n\pi x}{10}\right) = 50.$$

This is a Fourier sine series for the constant $50$ on $[0, 10]$. The coefficient of $\sin(n\pi x/10)$ in the Fourier series equals
$$A_n := b_n(1 - e^{-4n\pi}).$$

### E.2.10 Compute the Fourier coefficient $A_n$

By the Fourier sine series formula, for $f(x) = 50$ on $[0, 10]$:
$$A_n = \frac{2}{10}\int_0^{10} 50 \sin\!\left(\frac{n\pi x}{10}\right) dx = 10\int_0^{10}\sin\!\left(\frac{n\pi x}{10}\right) dx.$$
$$= 10 \cdot \left[-\frac{10}{n\pi}\cos\!\left(\frac{n\pi x}{10}\right)\right]_0^{10} = -\frac{100}{n\pi}[(-1)^n - 1] = \frac{100}{n\pi}[1 - (-1)^n].$$

Case-split:
- $n$ even: $A_n = 0$.
- $n$ odd: $A_n = 200/(n\pi)$.

### E.2.11 Solve for $b_n$

For odd $n$:
$$b_n = \frac{A_n}{1 - e^{-4n\pi}} = \frac{200}{n\pi(1 - e^{-4n\pi})}.$$

### E.2.12 Final solution

$$\boxed{u(x, y) = \frac{200}{\pi}\sum_{n\,\text{odd}} \frac{1}{n(1 - e^{-4n\pi})}\sin\!\left(\frac{n\pi x}{10}\right)\bigl[e^{-n\pi y/10} - e^{n\pi y/10 - 4n\pi}\bigr].}$$

### E.2.13 Sanity check

- $u(0, y) = 0$ ✓ (every sine vanishes).
- $u(10, y) = 0$ ✓.
- $u(x, 20) = 0$: at $y = 20$, the bracket is $e^{-2n\pi} - e^{2n\pi - 4n\pi} = e^{-2n\pi} - e^{-2n\pi} = 0$. ✓
- $u(x, 0) = 50$ for $0 < x < 10$ — checks out via the Fourier series.

---

## E.3 Sheet 1 Q9: Semi-infinite plate with linearly varying bottom temperature

### E.3.1 The problem

The same geometry as the lecture-note problem (semi-infinite, $0 \le x \le 10$, $0 \le y < \infty$, sides at $0°$, bounded at $\infty$), but the bottom edge has $u(x, 0) = f(x) = x$ instead of a constant. Find $u(x, y)$.

### E.3.2 Steps 1–7 — same as before

Everything up to the final boundary condition is identical. We get:
$$u(x, y) = \sum_{n=1}^\infty b_n\sin\!\left(\frac{n\pi x}{10}\right)e^{-n\pi y/10}.$$

### E.3.3 Apply the new bottom-edge condition

At $y = 0$:
$$u(x, 0) = \sum_n b_n\sin\!\left(\frac{n\pi x}{10}\right) = x.$$

This is a Fourier sine series for $f(x) = x$ on $[0, 10]$.

### E.3.4 Compute $b_n$ via integration by parts

$$b_n = \frac{2}{10}\int_0^{10} x\sin\!\left(\frac{n\pi x}{10}\right) dx = \frac{1}{5}\int_0^{10}x\sin\!\left(\frac{n\pi x}{10}\right) dx.$$

Use **integration by parts** $\int u\,dv = uv - \int v\,du$:
- Let $u = x$, so $du = dx$.
- Let $dv = \sin(n\pi x/10)\,dx$. Then $v = -\dfrac{10}{n\pi}\cos(n\pi x/10)$.

So:
$$\int_0^{10} x\sin\!\left(\frac{n\pi x}{10}\right) dx = \left[x \cdot\left(-\frac{10}{n\pi}\cos\frac{n\pi x}{10}\right)\right]_0^{10} - \int_0^{10}\left(-\frac{10}{n\pi}\cos\frac{n\pi x}{10}\right) dx.$$

**Evaluate the boundary term:**
- At $x = 10$: $-10\cdot\dfrac{10}{n\pi}\cos(n\pi) = -\dfrac{100}{n\pi}(-1)^n$.
- At $x = 0$: $0\cdot\dfrac{10}{n\pi}\cos(0) = 0$.
- Total boundary term: $-\dfrac{100}{n\pi}(-1)^n$.

**Evaluate the remaining integral:**
$$-\int_0^{10}\left(-\frac{10}{n\pi}\cos\frac{n\pi x}{10}\right) dx = \frac{10}{n\pi}\int_0^{10}\cos\!\left(\frac{n\pi x}{10}\right) dx.$$
$$= \frac{10}{n\pi}\cdot\left[\frac{10}{n\pi}\sin\!\left(\frac{n\pi x}{10}\right)\right]_0^{10} = \frac{100}{n^2\pi^2}\bigl[\sin(n\pi) - \sin(0)\bigr] = 0.$$

(The sine evaluates to zero at integer multiples of $\pi$.)

**Combine:**
$$\int_0^{10} x\sin\!\left(\frac{n\pi x}{10}\right) dx = -\frac{100}{n\pi}(-1)^n + 0 = -\frac{100(-1)^n}{n\pi}.$$

Now multiply by $1/5$ for $b_n$:
$$b_n = \frac{1}{5}\cdot\left(-\frac{100(-1)^n}{n\pi}\right) = -\frac{20(-1)^n}{n\pi}.$$

Rewrite the alternating sign more cleanly: $-(-1)^n = (-1)^{n+1}$:
$$b_n = \frac{20(-1)^{n+1}}{n\pi}.$$

### E.3.5 Final solution

$$\boxed{u(x, y) = \frac{20}{\pi}\sum_{n=1}^\infty \frac{(-1)^{n+1}}{n}\sin\!\left(\frac{n\pi x}{10}\right) e^{-n\pi y/10}.}$$

(This matches the answer in the problem sheet.)

### E.3.6 Quick sanity check
- $u(0, y) = 0$ and $u(10, y) = 0$ from the sines. ✓
- $u(x, \infty) = 0$ from the exponentials. ✓
- $u(x, 0)$: this is the Fourier sine series of $x$, which equals $x$ on the open interval $(0, 10)$. ✓

---

## E.4 Sheet 1 Q10: Separation of variables for Laplace's equation in plane polar coordinates

### E.4.1 The problem

Assume $u(\rho, \phi) = P(\rho)\,\Phi(\phi)$ and split Laplace's equation in plane polar coordinates into two independent ODEs.

### E.4.2 Setup

Laplace's equation in plane polar coordinates (no $z$ dependence — this is 2D):
$$\nabla^2 u = \frac{1}{\rho}\frac{\partial}{\partial \rho}\!\left(\rho\frac{\partial u}{\partial \rho}\right) + \frac{1}{\rho^2}\frac{\partial^2 u}{\partial \phi^2} = 0.$$

### E.4.3 Substitute the separable form

With $u = P(\rho)\Phi(\phi)$:
- $\dfrac{\partial u}{\partial \rho} = P'(\rho)\Phi(\phi)$.
- $\dfrac{\partial}{\partial \rho}\!\left(\rho\dfrac{\partial u}{\partial \rho}\right) = \Phi(\phi)\dfrac{d}{d\rho}\bigl[\rho P'(\rho)\bigr]$.
- $\dfrac{\partial^2 u}{\partial \phi^2} = P(\rho)\,\Phi''(\phi)$.

Substitute:
$$\frac{1}{\rho}\Phi(\phi)\frac{d}{d\rho}\bigl[\rho P'(\rho)\bigr] + \frac{1}{\rho^2}P(\rho)\Phi''(\phi) = 0.$$

### E.4.4 Multiply through by $\rho^2/(P\Phi)$

This is the algebraic move that separates the variables:
$$\frac{\rho}{P(\rho)}\frac{d}{d\rho}\bigl[\rho P'(\rho)\bigr] + \frac{\Phi''(\phi)}{\Phi(\phi)} = 0.$$

Rearrange:
$$\frac{\rho}{P}\frac{d}{d\rho}\bigl[\rho P'\bigr] = -\frac{\Phi''}{\Phi}.$$

### E.4.5 The separation argument

Left side: depends only on $\rho$. Right side: depends only on $\phi$. The only way for them to be equal across the whole domain is for both to equal a common constant. Call it $\lambda$ (or, conventionally for this problem, $m^2$):
$$\frac{\rho}{P}\frac{d}{d\rho}\bigl[\rho P'\bigr] = -\frac{\Phi''}{\Phi} = m^2.$$

Why $m^2$? Because the angular ODE will need to give us periodic functions ($\Phi(\phi) = \Phi(\phi + 2\pi)$), which forces sines and cosines, which need $\Phi'' = -m^2\Phi$ with $m \in \mathbb{Z}$.

### E.4.6 The two ODEs

**Angular:** $\Phi'' + m^2\Phi = 0$.
General solution: $\Phi(\phi) = E\cos(m\phi) + F\sin(m\phi)$ (or equivalently $\Phi = e^{\pm im\phi}$).
Periodicity $\Phi(\phi + 2\pi) = \Phi(\phi)$ forces $m$ to be an integer.

**Radial:** $\dfrac{\rho}{P}\dfrac{d}{d\rho}\bigl[\rho P'\bigr] = m^2$, or expanding:
$$\rho\frac{d}{d\rho}(\rho P') = m^2 P \;\Longrightarrow\; \rho^2 P'' + \rho P' - m^2 P = 0.$$

This is the **Cauchy–Euler equation**. Its solutions are power-law functions $P(\rho) = \rho^s$. Substituting:
$$\rho^2\cdot s(s-1)\rho^{s-2} + \rho\cdot s\rho^{s-1} - m^2\rho^s = \rho^s\bigl[s(s-1) + s - m^2\bigr] = \rho^s(s^2 - m^2) = 0.$$

So $s = \pm m$. The general radial solution is
$$P(\rho) = G\rho^m + H\rho^{-m} \quad (\text{for } m \neq 0).$$
For $m = 0$, the equation $\rho^2 P'' + \rho P' = 0$ has solutions $P(\rho) = G + H\ln\rho$.

### E.4.7 General solution

Combining and superposing:
$$u(\rho, \phi) = \bigl(G_0 + H_0\ln\rho\bigr) + \sum_{m=1}^\infty\bigl(G_m\rho^m + H_m\rho^{-m}\bigr)\bigl(E_m\cos m\phi + F_m\sin m\phi\bigr).$$

The constants are determined by boundary conditions. For example:
- If the domain *includes* the origin, we discard the $\rho^{-m}$ and $\ln\rho$ terms (they blow up at $\rho = 0$).
- If the domain extends to $\rho = \infty$, we may discard $\rho^m$ terms.

### E.4.8 Pattern to remember

In polar coordinates, Laplace separates into:
- Sines/cosines (or exponentials) in the angular direction (must be $2\pi$-periodic, forcing integer $m$).
- Power laws $\rho^m$ and $\rho^{-m}$ in the radial direction (Cauchy–Euler).

In contrast, the *wave* equation in polar coordinates gives **Bessel's equation** in the radial direction (more on this if you encounter circular drumheads).

---

# Part F — Separation of Variables: The Wave Equation

## F.1 The general framework

The 1D wave equation is $u_{tt} = v^2 u_{xx}$. We try $u(x, t) = X(x) T(t)$, substitute, and divide by $XT$:
$$X(x)T''(t) = v^2 X''(x)T(t) \;\Longrightarrow\; \frac{T''(t)}{v^2 T(t)} = \frac{X''(x)}{X(x)}.$$

LHS depends only on $t$, RHS only on $x$. Both equal a separation constant. The natural choice for problems with bounded space and homogeneous endpoint conditions is **$-k^2$**:
$$\frac{X''}{X} = -k^2, \qquad \frac{T''}{v^2 T} = -k^2.$$

This gives:
$$X'' + k^2 X = 0 \;\Rightarrow\; X(x) = A\cos(kx) + B\sin(kx),$$
$$T'' + k^2 v^2 T = 0 \;\Rightarrow\; T(t) = C\cos(\omega t) + D\sin(\omega t), \qquad \omega = kv.$$

The general separated solution is
$$u(x, t) = \bigl[A\cos(kx) + B\sin(kx)\bigr]\bigl[C\cos(\omega t) + D\sin(\omega t)\bigr].$$

### F.1.1 The two standard "plucked / struck" cases

For a string fixed at $x = 0$ and $x = L$:
- $u(0, t) = 0$ → $A = 0$.
- $u(L, t) = 0$ → $\sin(kL) = 0 \Rightarrow k = n\pi/L$.

So the spatial part becomes $\sin(n\pi x/L)$ as expected.

The time part depends on the *initial conditions*:

**Plucked from rest** (Cauchy IC: initial displacement, zero initial velocity):
- $u(x, 0) = f(x)$ given.
- $u_t(x, 0) = 0 \Rightarrow$ the $\sin$ time-component must vanish (since its time derivative is the cosine, evaluated to 1 at $t=0$). So $D = 0$.
- Solution: $u(x, t) = \sum_n B_n \sin(n\pi x/L)\cos(n\pi v t/L)$, with $B_n$ Fourier coefficients of $f$.

**Struck from rest** (Cauchy IC: zero initial displacement, initial velocity given):
- $u(x, 0) = 0 \Rightarrow$ the cosine time-component must vanish. So $C = 0$.
- $u_t(x, 0) = g(x)$ given.
- Solution: $u(x, t) = \sum_n B_n \sin(n\pi x/L)\sin(n\pi v t/L)$. Differentiating in $t$ and setting $t = 0$ gives $B_n \cdot (n\pi v/L)$ as the Fourier coefficient of $g(x)$.

These two cases cover essentially all the wave-equation problems on the sheets.

---

## F.2 Sheet 1 Q11: Plucked string, length 0.5 m, ramp profile

### F.2.1 The problem

A string of length 0.5 m is fixed at both ends and plucked from rest with initial displacement
$$u(x, 0) = \begin{cases} 0.05x & 0 < x < 0.2 \\ 0 & 0.2 \le x \le 0.5\end{cases}$$
Find the displacement $u(x, t)$ for $t > 0$.

**Important correction:** the function written here is a one-sided ramp followed by a jump to zero at $x=0.2$, not a true triangular pluck. The calculations in this section are correct for the function as written. If the original problem sheet intended a triangular displacement, add a descending linear segment and recompute the Fourier coefficients.

### F.2.2 Set up the eigenfunction expansion

Length $L = 0.5$. So $n\pi/L = n\pi/0.5 = 2n\pi$. We use the "plucked from rest" framework:
$$u(x, t) = \sum_{n=1}^\infty A_n \sin(2n\pi x)\cos(2n\pi v t).$$

The coefficients $A_n$ are the Fourier sine coefficients of the initial displacement.

### F.2.3 Compute the Fourier coefficients

$$A_n = \frac{2}{L}\int_0^L f(x)\sin\!\left(\frac{n\pi x}{L}\right) dx = \frac{2}{0.5}\int_0^{0.5} f(x)\sin(2n\pi x) dx = 4\int_0^{0.5} f(x)\sin(2n\pi x) dx.$$

Since $f(x) = 0$ on $[0.2, 0.5]$, the integral reduces to $[0, 0.2]$ where $f(x) = 0.05x$:
$$A_n = 4\int_0^{0.2} 0.05x\sin(2n\pi x) dx = 0.2\int_0^{0.2} x\sin(2n\pi x) dx.$$

### F.2.4 Integration by parts

Compute $\int_0^{0.2} x\sin(2n\pi x) dx$.

Let $u = x$, $du = dx$. Let $dv = \sin(2n\pi x)dx$, so $v = -\dfrac{1}{2n\pi}\cos(2n\pi x)$.

$$\int_0^{0.2} x\sin(2n\pi x) dx = \left[-\frac{x}{2n\pi}\cos(2n\pi x)\right]_0^{0.2} + \int_0^{0.2}\frac{1}{2n\pi}\cos(2n\pi x) dx.$$

**Boundary term:**
- At $x = 0.2$: $-\dfrac{0.2}{2n\pi}\cos(0.4n\pi) = -\dfrac{0.1}{n\pi}\cos(0.4n\pi)$.
- At $x = 0$: $0$.

So the boundary term is $-\dfrac{0.1}{n\pi}\cos(0.4n\pi)$.

**Remaining integral:**
$$\int_0^{0.2}\frac{1}{2n\pi}\cos(2n\pi x) dx = \frac{1}{2n\pi}\cdot\left[\frac{\sin(2n\pi x)}{2n\pi}\right]_0^{0.2} = \frac{\sin(0.4n\pi)}{4n^2\pi^2}.$$

**Combined:**
$$\int_0^{0.2} x\sin(2n\pi x) dx = -\frac{0.1\cos(0.4n\pi)}{n\pi} + \frac{\sin(0.4n\pi)}{4n^2\pi^2}.$$

### F.2.5 Multiply by 0.2

$$A_n = 0.2\cdot\left[-\frac{0.1\cos(0.4n\pi)}{n\pi} + \frac{\sin(0.4n\pi)}{4n^2\pi^2}\right] = -\frac{0.02\cos(0.4n\pi)}{n\pi} + \frac{0.05\sin(0.4n\pi)}{n^2\pi^2}.$$

Cleaner:
$$A_n = \frac{0.05\sin(0.4n\pi)}{n^2\pi^2} - \frac{0.02\cos(0.4n\pi)}{n\pi}.$$

### F.2.6 Final solution

$$\boxed{u(x, t) = \sum_{n=1}^\infty\left[\frac{0.05\sin(0.4n\pi)}{n^2\pi^2} - \frac{0.02\cos(0.4n\pi)}{n\pi}\right]\sin(2n\pi x)\cos(2n\pi v t).}$$

---

## F.3 Sheet 1 Q12: Plucked string with cubic profile

### F.3.1 The problem

A string of length $\pi$ m is fixed at the ends and plucked from rest with $u(x, 0) = 0.1x(\pi^2 - x^2)$. Find $u(x, t)$ for $t > 0$.

(Note: the problem sheet's text "string of length m" has a typo — the length must be $\pi$ because that's where the displacement function vanishes naturally, giving us our boundary conditions for free.)

### F.3.2 Setup

Length $L = \pi$. So $n\pi/L = n$. Plucked from rest:
$$u(x, t) = \sum_{n=1}^\infty A_n\sin(nx)\cos(nvt).$$

$$A_n = \frac{2}{\pi}\int_0^\pi 0.1\,x(\pi^2 - x^2)\sin(nx) dx = \frac{0.2}{\pi}\int_0^\pi (\pi^2 x - x^3)\sin(nx) dx.$$

Split the integral into two pieces:
$$I_1 = \int_0^\pi x\sin(nx) dx, \qquad I_2 = \int_0^\pi x^3 \sin(nx) dx.$$

So $A_n = \dfrac{0.2}{\pi}(\pi^2 I_1 - I_2)$.

### F.3.3 Compute $I_1$ by parts

$u = x$, $du = dx$. $dv = \sin(nx) dx$, $v = -\cos(nx)/n$.
$$I_1 = \left[-\frac{x\cos(nx)}{n}\right]_0^\pi + \int_0^\pi\frac{\cos(nx)}{n} dx = -\frac{\pi(-1)^n}{n} + \frac{1}{n}\left[\frac{\sin(nx)}{n}\right]_0^\pi = -\frac{\pi(-1)^n}{n}.$$

(The remaining integral involves $\sin(n\pi) - \sin(0) = 0$.)

### F.3.4 Compute $I_2$ by repeated integration by parts (tabular method)

The tabular method: differentiate $x^3$ repeatedly and integrate $\sin(nx)$ repeatedly, alternating signs.

| Sign | Diff of $x^3$ | Integral of $\sin(nx)$ |
|---|---|---|
| $+$ | $x^3$ | $-\cos(nx)/n$ |
| $-$ | $3x^2$ | $-\sin(nx)/n^2$ |
| $+$ | $6x$ | $\cos(nx)/n^3$ |
| $-$ | $6$ | $\sin(nx)/n^4$ |
| stop | $0$ |  |

Read off the antiderivative by multiplying along the diagonals:
$$\int x^3\sin(nx) dx = -\frac{x^3\cos(nx)}{n} + \frac{3x^2\sin(nx)}{n^2} + \frac{6x\cos(nx)}{n^3} - \frac{6\sin(nx)}{n^4} + C.$$

Now evaluate at the limits.

**At $x = \pi$:**
- $-\dfrac{\pi^3\cos(n\pi)}{n} = -\dfrac{\pi^3(-1)^n}{n}$.
- $\dfrac{3\pi^2\sin(n\pi)}{n^2} = 0$.
- $\dfrac{6\pi\cos(n\pi)}{n^3} = \dfrac{6\pi(-1)^n}{n^3}$.
- $-\dfrac{6\sin(n\pi)}{n^4} = 0$.

**At $x = 0$:** all terms have either $x$ or $\sin(0)$ factors, so all evaluate to 0.

So:
$$I_2 = -\frac{\pi^3(-1)^n}{n} + \frac{6\pi(-1)^n}{n^3}.$$

### F.3.5 Combine

$$\pi^2 I_1 - I_2 = \pi^2\cdot\left(-\frac{\pi(-1)^n}{n}\right) - \left(-\frac{\pi^3(-1)^n}{n} + \frac{6\pi(-1)^n}{n^3}\right)$$
$$= -\frac{\pi^3(-1)^n}{n} + \frac{\pi^3(-1)^n}{n} - \frac{6\pi(-1)^n}{n^3}$$
$$= -\frac{6\pi(-1)^n}{n^3} = \frac{6\pi(-1)^{n+1}}{n^3}.$$

The $\pi^3 (-1)^n / n$ terms beautifully cancel.

### F.3.6 Compute $A_n$

$$A_n = \frac{0.2}{\pi}\cdot\frac{6\pi(-1)^{n+1}}{n^3} = \frac{1.2(-1)^{n+1}}{n^3}.$$

### F.3.7 Final solution

$$\boxed{u(x, t) = 1.2\sum_{n=1}^\infty\frac{(-1)^{n+1}}{n^3}\sin(nx)\cos(nvt).}$$

### F.3.8 Why this answer is so clean

The cubic initial profile $x(\pi^2 - x^2)$ already vanishes at $x = 0$ and $x = \pi$, matching the boundary conditions. It is also a smooth function that's nicely compatible with the sine basis. The $1/n^3$ decay of the coefficients tells us the series converges fast — a sign of a smooth initial condition.

---

# Part G — Schrödinger's Equation by Separation of Variables

## G.1 Sheet 2 Q1: Particle in a 1D infinite well

### G.1.1 The problem

Find the general solution to the time-independent Schrödinger equation for an electron of mass $m$ confined within a 1D well of width $L$ with impenetrable walls.

### G.1.2 The setup

The 1D time-independent Schrödinger equation (TISE) is
$$-\frac{\hbar^2}{2m}\frac{d^2\psi(x)}{dx^2} + V(x)\psi(x) = E\psi(x).$$

The walls are "impenetrable" means the potential is infinite outside the well:
$$V(x) = \begin{cases} 0, & 0 < x < L \\ \infty, & x \le 0 \text{ or } x \ge L\end{cases}$$

Physical interpretation: the particle can never be found in the wall regions because the energy required would be infinite. So $\psi(x) = 0$ for $x \le 0$ and $x \ge L$.

For continuity, we require:
$$\psi(0) = 0, \qquad \psi(L) = 0.$$

These are our two boundary conditions.

### G.1.3 Solve inside the well

Inside the well, $V = 0$, and the TISE simplifies to
$$-\frac{\hbar^2}{2m}\frac{d^2\psi}{dx^2} = E\psi.$$

Rearrange:
$$\frac{d^2\psi}{dx^2} = -\frac{2mE}{\hbar^2}\psi.$$

Define $k^2 = \dfrac{2mE}{\hbar^2}$. In an infinite square well with the potential floor taken as zero, non-trivial eigenstates have $E>0$. If $E<0$, the spatial solution is hyperbolic/exponential, and the boundary conditions $\psi(0)=\psi(L)=0$ force only the trivial solution. Thus we proceed with $E>0$. Then
$$\psi'' = -k^2\psi.$$

The general solution is
$$\psi(x) = A\sin(kx) + B\cos(kx).$$

### G.1.4 Apply boundary conditions

**$\psi(0) = 0$:**
$$\psi(0) = A\sin(0) + B\cos(0) = 0 + B = B.$$
So $B = 0$. Solution becomes $\psi(x) = A\sin(kx)$.

**$\psi(L) = 0$:**
$$\psi(L) = A\sin(kL) = 0.$$
We don't want $A = 0$ (gives $\psi \equiv 0$, no particle, trivial). So we need $\sin(kL) = 0$, hence
$$kL = n\pi \;\Longrightarrow\; k = \frac{n\pi}{L}, \qquad n = 1, 2, 3, \ldots$$

(We exclude $n = 0$ because that gives the trivial solution; negative $n$ give the same set of eigenfunctions up to a sign that's absorbed into $A$.)

### G.1.5 Eigenfunctions and energy levels

**Eigenfunctions:**
$$\boxed{\psi_n(x) = A\sin\!\left(\frac{n\pi x}{L}\right).}$$

The constant $A$ is fixed by **normalisation** (total probability of finding the particle is 1):
$$\int_0^L |\psi_n|^2 dx = 1 \;\Longrightarrow\; A^2\int_0^L\sin^2\!\left(\frac{n\pi x}{L}\right) dx = 1.$$
$$\int_0^L\sin^2\!\left(\frac{n\pi x}{L}\right) dx = \frac{L}{2}\;\;\text{(standard half-period result)} \;\Longrightarrow\; A = \sqrt{\frac{2}{L}}.$$

**Energy levels:** Substitute $k = n\pi/L$ back into $k^2 = 2mE/\hbar^2$:
$$E_n = \frac{\hbar^2 k^2}{2m} = \boxed{\frac{n^2\pi^2\hbar^2}{2mL^2}.}$$

### G.1.6 Pattern to remember

The infinite-well problem is *mathematically identical* to a vibrating string with fixed ends — the same ODE, the same boundary conditions, the same eigenfunctions and quantised eigenvalues. This isn't a coincidence: both are described by linear PDEs with homogeneous Dirichlet boundary conditions.

---

## G.2 Sheet 2 Q2: Particle in a 3D rectangular box

### G.2.1 The problem

Find the energies of an electron in a quantum well described by a rectangular box with sides $L_x \times L_y \times L_z$ and impenetrable walls.

### G.2.2 The 3D TISE inside the box

With $V = 0$ inside:
$$-\frac{\hbar^2}{2m}\nabla^2\psi(x, y, z) = E\psi(x, y, z),$$
which expands to
$$-\frac{\hbar^2}{2m}\left(\frac{\partial^2\psi}{\partial x^2} + \frac{\partial^2\psi}{\partial y^2} + \frac{\partial^2\psi}{\partial z^2}\right) = E\psi.$$

### G.2.3 Try a separable solution

Let $\psi(x, y, z) = X(x)Y(y)Z(z)$. The Laplacian becomes
$$\nabla^2\psi = X''(x)Y(y)Z(z) + X(x)Y''(y)Z(z) + X(x)Y(y)Z''(z).$$

Substitute and divide by $XYZ$:
$$-\frac{\hbar^2}{2m}\left[\frac{X''}{X} + \frac{Y''}{Y} + \frac{Z''}{Z}\right] = E.$$

Each ratio depends on only one variable, but their sum is constant. So each individual term must be a constant. Define:
$$-\frac{\hbar^2}{2m}\frac{X''}{X} = E_x, \quad -\frac{\hbar^2}{2m}\frac{Y''}{Y} = E_y, \quad -\frac{\hbar^2}{2m}\frac{Z''}{Z} = E_z,$$
with the constraint
$$E_x + E_y + E_z = E.$$

### G.2.4 Three identical 1D problems

Each separated equation is identical in form to the 1D infinite well from Section G.1, just along a different axis. By the same argument:

For $X$:
- $X(0) = X(L_x) = 0$ → $X(x) = A_x\sin(n_x\pi x/L_x)$.
- $E_x = \dfrac{n_x^2\pi^2\hbar^2}{2mL_x^2}$, $n_x = 1, 2, 3, \ldots$

For $Y$:
- $Y(y) = A_y\sin(n_y\pi y/L_y)$, $E_y = \dfrac{n_y^2\pi^2\hbar^2}{2mL_y^2}$.

For $Z$:
- $Z(z) = A_z\sin(n_z\pi z/L_z)$, $E_z = \dfrac{n_z^2\pi^2\hbar^2}{2mL_z^2}$.

### G.2.5 Total energy

$$\boxed{E_{n_x, n_y, n_z} = \frac{\pi^2\hbar^2}{2m}\left(\frac{n_x^2}{L_x^2} + \frac{n_y^2}{L_y^2} + \frac{n_z^2}{L_z^2}\right), \quad n_x, n_y, n_z = 1, 2, 3, \ldots}$$

### G.2.6 The wavefunction

$$\psi_{n_x, n_y, n_z}(x, y, z) = \sqrt{\frac{8}{L_x L_y L_z}}\sin\!\left(\frac{n_x\pi x}{L_x}\right)\sin\!\left(\frac{n_y\pi y}{L_y}\right)\sin\!\left(\frac{n_z\pi z}{L_z}\right).$$

(The normalisation constant comes from $\int|\psi|^2 d^3r = 1$ — the product of three independent normalisations of $\sqrt{2/L_i}$.)

### G.2.7 Degeneracy

For a *cubic* box ($L_x = L_y = L_z = L$), states with different $(n_x, n_y, n_z)$ that share the same value of $n_x^2 + n_y^2 + n_z^2$ have the same energy. They are called **degenerate** states. For example:
- $(1, 1, 2), (1, 2, 1), (2, 1, 1)$ all have $n_x^2 + n_y^2 + n_z^2 = 6$ → triple-degenerate.

This degeneracy is broken if the box dimensions are unequal.

---

## G.3 Sheet 2 Q3: 1D rod connected to heat baths at both ends

This is one of the most important problems on the sheets — it shows how to handle **inhomogeneous boundary conditions** with separation of variables.

### G.3.1 The problem

A 1D rod of length $L$ has its ends maintained at temperatures $T_1$ at $x = 0$ and $T_2$ at $x = L$. The temperature evolves according to the heat equation
$$\kappa\frac{\partial^2 u(x, t)}{\partial x^2} = \frac{\partial u(x, t)}{\partial t}. \quad (\text{H})$$

Three parts to the problem:
- (a) Show that the steady-state solution is $u_{eq}(x) = T_1 + (T_2 - T_1)\dfrac{x}{L}$.
- (b) If $u_0(x, t)$ solves (H) with homogeneous boundary conditions $u_0(0, t) = u_0(L, t) = 0$, show that $u(x, t) = u_0(x, t) + u_{eq}(x)$ also solves (H), and find its boundary conditions.
- (c) Given a series form for $u_0$, derive the full solution and the formula for the Fourier coefficients $b_n$.

### G.3.2 Part (a) — Steady-state solution

In thermal equilibrium, the temperature distribution doesn't change with time:
$$\frac{\partial u}{\partial t} = 0.$$

Substitute into (H):
$$\kappa\frac{d^2 u_{eq}}{dx^2} = 0 \;\Longrightarrow\; \frac{d^2 u_{eq}}{dx^2} = 0.$$

Integrate twice:
$$u_{eq}(x) = C_1 x + C_2.$$

Apply the boundary conditions:
- At $x = 0$: $u_{eq}(0) = T_1 \Rightarrow C_2 = T_1$.
- At $x = L$: $u_{eq}(L) = T_2 \Rightarrow C_1 L + T_1 = T_2 \Rightarrow C_1 = (T_2 - T_1)/L$.

So:
$$\boxed{u_{eq}(x) = T_1 + (T_2 - T_1)\frac{x}{L}.}$$

This is just a linear interpolation between the two end temperatures, which is intuitive: heat flows from hot to cold, and at equilibrium the temperature gradient is constant.

### G.3.3 Part (b) — Show the superposition is a solution

Define $u(x, t) = u_0(x, t) + u_{eq}(x)$. We need to show this satisfies (H) and find its boundary conditions.

**LHS of (H):**
$$\kappa\frac{\partial^2 u}{\partial x^2} = \kappa\frac{\partial^2}{\partial x^2}(u_0 + u_{eq}) = \kappa u_{0,xx} + \kappa u_{eq,xx}.$$
The second term is zero (since $u_{eq}$ is the steady state, it satisfies $u_{eq,xx} = 0$). So LHS = $\kappa u_{0,xx}$.

**RHS of (H):**
$$\frac{\partial u}{\partial t} = \frac{\partial}{\partial t}(u_0 + u_{eq}) = u_{0,t} + u_{eq,t}.$$
The second term is zero (since $u_{eq}$ doesn't depend on time). So RHS = $u_{0,t}$.

Equating: LHS = RHS becomes $\kappa u_{0,xx} = u_{0,t}$, which is precisely (H) with $u$ replaced by $u_0$. Since $u_0$ is given to be a solution of (H), this is satisfied. ✓

So $u = u_0 + u_{eq}$ is also a solution.

**Boundary conditions for $u(x, t)$:**
- At $x = 0$: $u(0, t) = u_0(0, t) + u_{eq}(0) = 0 + T_1 = T_1$.
- At $x = L$: $u(L, t) = u_0(L, t) + u_{eq}(L) = 0 + T_2 = T_2$.

So $u$ satisfies the original (inhomogeneous) boundary conditions $u(0, t) = T_1$ and $u(L, t) = T_2$. ✓

### G.3.4 Why this matters

This is the **standard trick** for handling inhomogeneous boundary conditions:

1. Find the steady-state solution $u_{eq}$ that satisfies the inhomogeneous boundary conditions.
2. Subtract it off, leaving a *transient* part $u_0 = u - u_{eq}$ that satisfies the *homogeneous* boundary conditions.
3. Solve for $u_0$ by ordinary separation of variables (which works cleanly with homogeneous BCs).
4. Add back: $u = u_0 + u_{eq}$.

### G.3.5 Part (c) — Full Fourier series solution

We're given the form of the transient:
$$u_0(x, t) = \sum_{n=1}^\infty b_n\sin\!\left(\frac{n\pi x}{L}\right)\exp\!\left[-\frac{n^2\pi^2}{L^2}\kappa t\right].$$

(This comes from separating variables on the homogeneous heat-equation problem — sines in space because of the homogeneous BCs, decaying exponentials in time because the heat equation is dissipative.)

The full solution is:
$$u(x, t) = u_{eq}(x) + u_0(x, t) = T_1 + (T_2 - T_1)\frac{x}{L} + \sum_{n=1}^\infty b_n\sin\!\left(\frac{n\pi x}{L}\right)\exp\!\left[-\frac{n^2\pi^2}{L^2}\kappa t\right].$$

Apply the **initial condition** $u(x, 0) = f(x)$:
$$f(x) = T_1 + (T_2 - T_1)\frac{x}{L} + \sum_{n=1}^\infty b_n\sin\!\left(\frac{n\pi x}{L}\right)\cdot 1.$$

Rearrange:
$$f(x) - T_1 - (T_2 - T_1)\frac{x}{L} = \sum_{n=1}^\infty b_n\sin\!\left(\frac{n\pi x}{L}\right).$$

This is a Fourier sine series for the function $\bigl[f(x) - T_1 - (T_2-T_1)x/L\bigr]$ on $[0, L]$. The coefficients are:

$$\boxed{b_n = \frac{2}{L}\int_0^L\sin\!\left(\frac{n\pi x}{L}\right)\left[f(x) - T_1 - (T_2 - T_1)\frac{x}{L}\right] dx.}$$

### G.3.6 Long-time behaviour

As $t \to \infty$, every exponential $e^{-n^2\pi^2\kappa t/L^2}$ decays to 0. So the transient $u_0$ vanishes, leaving
$$u(x, t)\to u_{eq}(x) = T_1 + (T_2 - T_1)\frac{x}{L}.$$

The rod relaxes exponentially to the linear equilibrium profile, regardless of the initial state. The slowest-decaying mode is $n = 1$ with decay rate $\pi^2\kappa/L^2$, which sets the dominant time scale for relaxation.

---

# Part H — The Dirac Delta Function (Sheet 2 Q4)

## H.1 The problem

What is the Dirac delta function and how can it be defined? Why is it useful in physical problems?

## H.2 The intuitive picture

Imagine a function $f_L(x)$ that is a "top hat":
$$f_L(x) = \begin{cases} 1/L & \text{if } |x| \le L/2 \\ 0 & \text{otherwise}\end{cases}$$

This is normalised: $\int_{-\infty}^\infty f_L(x) dx = 1$ (the rectangle has width $L$ and height $1/L$, total area 1).

Now imagine **shrinking $L$ to zero**. As $L$ decreases, the top hat becomes narrower (width $L$) but taller (height $1/L$). The area always remains exactly 1.

In the limit $L \to 0$, we get a function that is:
- Zero everywhere except at $x = 0$.
- Infinitely tall at $x = 0$.
- Has total area 1.

This idealised "function" is the **Dirac delta**, denoted $\delta(x)$.

## H.3 Formal definition

Strictly speaking, $\delta(x)$ is not a function — it's a *generalised function* or *distribution*. The formal definitions:

**Definition 1 (limit of peaks):**
$$\delta(x) = \lim_{L \to 0} f_L(x)$$
for any sequence of normalised peak functions (top hat, Lorentzian, Gaussian — they all give the same $\delta$).

**Definition 2 (defining properties):**
$$\delta(x) = 0 \text{ for } x \ne 0, \qquad \int_{-\infty}^\infty\delta(x) dx = 1.$$

**Definition 3 (sifting property — the most useful):**
For any continuous function $g$:
$$\int_{-\infty}^\infty g(x)\delta(x - x_0) dx = g(x_0).$$

The sifting property is so important we should make sure we believe it. Using the top-hat picture:
$$\int_{-\infty}^\infty g(x)\delta(x - x_0) dx = \lim_{L\to 0}\int_{x_0 - L/2}^{x_0 + L/2}\frac{g(x)}{L} dx \approx \lim_{L\to 0}\frac{1}{L}\cdot L\cdot g(x_0) = g(x_0).$$

The integral picks out — "sifts" — the value of $g$ at the location $x_0$ where the spike sits.

## H.4 Other sequences that converge to $\delta$

- **Lorentzian:** $\dfrac{1}{\pi}\dfrac{L}{x^2 + L^2}$ as $L \to 0$.
- **Gaussian:** $\dfrac{1}{\sqrt{2\pi}L}e^{-x^2/(2L^2)}$ as $L \to 0$.

The Gaussian limit is particularly natural in physics because the fundamental solution of the diffusion equation is a Gaussian whose width shrinks to zero as $t \to 0$.

## H.5 Useful Fourier transform of $\delta$

Using the sifting property:
$$\mathcal{F}[\delta(x - x_0)](k) = \frac{1}{\sqrt{2\pi}}\int_{-\infty}^\infty\delta(x - x_0)e^{-ikx} dx = \frac{1}{\sqrt{2\pi}}e^{-ikx_0}.$$

In particular for $x_0 = 0$:
$$\mathcal{F}[\delta(x)] = \frac{1}{\sqrt{2\pi}}.$$

So a delta function in real space transforms to a constant in Fourier space — physically, an infinitely sharp spike requires infinitely many frequencies to construct.

## H.6 Why is it useful in physical problems?

### H.6.1 Idealisation of point sources

Many physical situations involve forces or sources concentrated at a single point. Mathematically idealising them as delta functions makes the algebra clean:
- A point charge $Q$ at the origin: charge density $\rho(\mathbf{r}) = Q\delta(\mathbf{r}) = Q\delta(x)\delta(y)\delta(z)$ in 3D.
- A point mass: mass density $\rho(\mathbf{r}) = M\delta(\mathbf{r})$.
- An impulsive force: force per unit time $F\delta(t)$ — a sudden hit at $t = 0$.

### H.6.2 Green's functions

The whole technology of Green's functions is built around the delta. Given a linear PDE $\mathcal{L}u = f$, the Green's function $G(\mathbf{r}, \mathbf{r}')$ is defined by
$$\mathcal{L}G = \delta(\mathbf{r} - \mathbf{r}').$$

This says $G$ is the *response* to a unit point source. Once you have $G$, the response to any distributed source $f$ can be computed by integrating:
$$u(\mathbf{r}) = \int G(\mathbf{r}, \mathbf{r}')f(\mathbf{r}') d\mathbf{r}'.$$

This works because a general $f$ can be decomposed as a superposition of delta functions:
$$f(\mathbf{r}) = \int f(\mathbf{r}')\delta(\mathbf{r} - \mathbf{r}') d\mathbf{r}'$$
(another use of the sifting property).

### H.6.3 Initial / boundary conditions

The fundamental solution of the diffusion equation
$$c(x, y, t) = \frac{1}{4\pi Dt}e^{-(x^2 + y^2)/(4Dt)}$$
arises precisely from solving the heat equation with the initial condition $c(x, y, 0) = \delta(x)\delta(y)$ — an instantaneous, perfectly localised source.

### H.6.4 Pattern to remember

When you encounter:
- "an instantaneous force" → $\delta(t - t_0)$.
- "a localised source at one point" → $\delta(\mathbf{r} - \mathbf{r}_0)$.
- "the response of a linear system to..." → reach for Green's functions.

---

# Part I — Fourier Sine and Cosine Transforms

## I.1 The definitions

For a function $f$ defined on $0 \le x < \infty$:
$$\mathcal{S}[f](\omega) = S(\omega) = \sqrt{\frac{2}{\pi}}\int_0^\infty f(x)\sin(\omega x) dx,$$
$$\mathcal{C}[f](\omega) = C(\omega) = \sqrt{\frac{2}{\pi}}\int_0^\infty f(x)\cos(\omega x) dx.$$

The inverse transforms have the same form (these transforms are self-inverse with this normalisation):
$$f(x) = \sqrt{\frac{2}{\pi}}\int_0^\infty S(\omega)\sin(\omega x) d\omega,$$
$$f(x) = \sqrt{\frac{2}{\pi}}\int_0^\infty C(\omega)\cos(\omega x) d\omega.$$

## I.2 When to use which

- **Sine transform** is best when *Dirichlet* boundary data is given at $x = 0$ (i.e. $f(0)$ is known). Why? Because $\sin(0) = 0$ kills any boundary terms involving $f(0)$ in integration by parts — except where they're useful.

- **Cosine transform** is best when *Neumann* boundary data is given at $x = 0$ (i.e. $f'(0)$ is known). Why? Because $\cos(0) = 1$ keeps boundary terms involving $f(0)$, but the derivative of cosine introduces a sine which kills $f'(0)$ boundary terms.

This will become crystal clear once we derive the derivative properties.

## I.3 Sheet 2 Q5: Derivative properties

Assume $f(x) \to 0$ and $f'(x) \to 0$ as $x \to \infty$ (decay at infinity, common in physics problems).

### I.3.1 Part (a): Prove $\mathcal{S}[f'](\omega) = -\omega\,\mathcal{C}[f](\omega)$

**Setup:**
$$\mathcal{S}[f'] = \sqrt{\frac{2}{\pi}}\int_0^\infty f'(x)\sin(\omega x) dx.$$

**Integration by parts.** Choose $u = \sin(\omega x)$, $dv = f'(x) dx$. Then $du = \omega\cos(\omega x) dx$, $v = f(x)$.

$$\int_0^\infty f'(x)\sin(\omega x) dx = \bigl[f(x)\sin(\omega x)\bigr]_0^\infty - \int_0^\infty f(x)\omega\cos(\omega x) dx.$$

**Evaluate the boundary term:**
- At $x \to \infty$: $f(x) \to 0$ (given), so $f(x)\sin(\omega x) \to 0$.
- At $x = 0$: $\sin(0) = 0$, so the term is $f(0)\cdot 0 = 0$.

Both boundary contributions vanish. So:
$$\int_0^\infty f'(x)\sin(\omega x) dx = -\omega\int_0^\infty f(x)\cos(\omega x) dx.$$

Multiply both sides by $\sqrt{2/\pi}$:
$$\mathcal{S}[f'](\omega) = -\omega\cdot\sqrt{\frac{2}{\pi}}\int_0^\infty f(x)\cos(\omega x) dx = -\omega\,\mathcal{C}[f](\omega). \;\;\checkmark$$

### I.3.2 Part (b): Prove $\mathcal{C}[f'](\omega) = -\sqrt{2/\pi}\,f(0) + \omega\,\mathcal{S}[f](\omega)$

**Setup:**
$$\mathcal{C}[f'] = \sqrt{\frac{2}{\pi}}\int_0^\infty f'(x)\cos(\omega x) dx.$$

**Integration by parts.** Choose $u = \cos(\omega x)$, $dv = f'(x) dx$. Then $du = -\omega\sin(\omega x) dx$, $v = f(x)$.

$$\int_0^\infty f'(x)\cos(\omega x) dx = \bigl[f(x)\cos(\omega x)\bigr]_0^\infty - \int_0^\infty f(x)\bigl(-\omega\sin(\omega x)\bigr) dx.$$

**Evaluate the boundary term:**
- At $x \to \infty$: $f(x) \to 0$, so the term vanishes.
- At $x = 0$: $f(0)\cos(0) = f(0)$.

Boundary contribution = $0 - f(0) = -f(0)$.

So:
$$\int_0^\infty f'\cos(\omega x) dx = -f(0) + \omega\int_0^\infty f(x)\sin(\omega x) dx.$$

Multiply by $\sqrt{2/\pi}$:
$$\mathcal{C}[f'](\omega) = -\sqrt{\frac{2}{\pi}}\,f(0) + \omega\cdot\sqrt{\frac{2}{\pi}}\int_0^\infty f\sin(\omega x) dx$$
$$= -\sqrt{\frac{2}{\pi}}\,f(0) + \omega\,\mathcal{S}[f](\omega). \;\;\checkmark$$

### I.3.3 Part (c): Prove $\mathcal{S}[f''] = \sqrt{2/\pi}\,\omega f(0) - \omega^2\mathcal{S}[f]$

**Strategy:** Apply Part (a) twice. First, treat $f''$ as the derivative of $f'$:
$$\mathcal{S}[f''] = \mathcal{S}[(f')'] = -\omega\,\mathcal{C}[f'].$$

Now substitute the result from Part (b):
$$\mathcal{S}[f''] = -\omega\left[-\sqrt{\frac{2}{\pi}}\,f(0) + \omega\,\mathcal{S}[f]\right] = \sqrt{\frac{2}{\pi}}\,\omega f(0) - \omega^2\mathcal{S}[f]. \;\;\checkmark$$

### I.3.4 Part (d): Prove $\mathcal{C}[f''] = -\sqrt{2/\pi}\,f'(0) - \omega^2\mathcal{C}[f]$

**Strategy:** Apply Part (b) treating $f''$ as the derivative of $f'$:
$$\mathcal{C}[f''] = \mathcal{C}[(f')'] = -\sqrt{\frac{2}{\pi}}\,f'(0) + \omega\,\mathcal{S}[f'].$$

Now substitute Part (a):
$$\mathcal{C}[f''] = -\sqrt{\frac{2}{\pi}}\,f'(0) + \omega\bigl(-\omega\,\mathcal{C}[f]\bigr) = -\sqrt{\frac{2}{\pi}}\,f'(0) - \omega^2\mathcal{C}[f]. \;\;\checkmark$$

### I.3.5 The crucial pattern

Look at the key formulas for second derivatives:
$$\mathcal{S}[f''] = \sqrt{\frac{2}{\pi}}\,\omega f(0) - \omega^2\mathcal{S}[f] \quad\leftarrow\text{ requires } f(0).$$
$$\mathcal{C}[f''] = -\sqrt{\frac{2}{\pi}}\,f'(0) - \omega^2\mathcal{C}[f] \quad\leftarrow\text{ requires } f'(0).$$

This is why your choice of transform should match your boundary data:
- Given $f(0)$ (Dirichlet) → use sine transform.
- Given $f'(0)$ (Neumann) → use cosine transform.

If you choose wrong, you end up needing boundary data you don't have!

---

## I.4 Sheet 2 Q6: Heat flow in a semi-infinite rod

### I.4.1 The problem

A semi-infinite rod ($0 \le x < \infty$) with thermal conductivity $\kappa$ is initially at uniform temperature $0°$. A constant heat flux $\lambda = -\kappa\partial u/\partial x$ (into the rod) is applied at the end $x = 0$. Show that
$$u(x, t) = \frac{2\lambda}{\pi}\int_0^\infty\frac{1 - e^{-\kappa\omega^2 t}}{\kappa\omega^2}\cos(\omega x) d\omega.$$

### I.4.2 Setup

The heat equation:
$$\frac{\partial u}{\partial t} = \kappa\frac{\partial^2 u}{\partial x^2}.$$

- Initial condition (IC): $u(x, 0) = 0$.
- Boundary condition (BC): heat flux into the rod at $x = 0$ is $\lambda$, i.e. $-\kappa u_x(0, t) = \lambda$, so $u_x(0, t) = -\lambda/\kappa$.

### I.4.3 Choose a transform

The boundary condition specifies the *derivative* $u_x(0, t)$ — this is **Neumann** data. So we use the **Fourier cosine transform** (the result from Part I.3.4 will involve $f'(0)$, which we know).

Define
$$U(\omega, t) = \mathcal{C}_x[u(x, t)] = \sqrt{\frac{2}{\pi}}\int_0^\infty u(x, t)\cos(\omega x) dx.$$

The cosine transform commutes with $\partial/\partial t$ (since $t$ is a parameter):
$$\mathcal{C}_x\!\left[\frac{\partial u}{\partial t}\right] = \frac{\partial U}{\partial t}.$$

For $\partial^2 u/\partial x^2$, use the result from Part I.3.4:
$$\mathcal{C}_x[u_{xx}] = -\sqrt{\frac{2}{\pi}}\,u_x(0, t) - \omega^2 U(\omega, t).$$

Substitute the boundary condition $u_x(0, t) = -\lambda/\kappa$:
$$\mathcal{C}_x[u_{xx}] = -\sqrt{\frac{2}{\pi}}\,\left(-\frac{\lambda}{\kappa}\right) - \omega^2 U = \sqrt{\frac{2}{\pi}}\,\frac{\lambda}{\kappa} - \omega^2 U.$$

### I.4.4 Transform the PDE

The heat equation becomes
$$\frac{\partial U}{\partial t} = \kappa\left[\sqrt{\frac{2}{\pi}}\,\frac{\lambda}{\kappa} - \omega^2 U\right] = \lambda\sqrt{\frac{2}{\pi}} - \kappa\omega^2 U.$$

This is a **linear first-order ODE** in $t$ (with $\omega$ as a parameter):
$$\frac{\partial U}{\partial t} + \kappa\omega^2 U = \lambda\sqrt{\frac{2}{\pi}}.$$

### I.4.5 Solve the ODE

Use the integrating factor method. The integrating factor is $\mu(t) = e^{\kappa\omega^2 t}$. Multiply both sides:
$$e^{\kappa\omega^2 t}\frac{\partial U}{\partial t} + \kappa\omega^2 e^{\kappa\omega^2 t}U = \lambda\sqrt{\frac{2}{\pi}}\,e^{\kappa\omega^2 t}.$$

The LHS is the derivative of a product:
$$\frac{\partial}{\partial t}\!\left[U\,e^{\kappa\omega^2 t}\right] = \lambda\sqrt{\frac{2}{\pi}}\,e^{\kappa\omega^2 t}.$$

Integrate with respect to $t$:
$$U\,e^{\kappa\omega^2 t} = \lambda\sqrt{\frac{2}{\pi}}\cdot\frac{e^{\kappa\omega^2 t}}{\kappa\omega^2} + K(\omega),$$
where $K(\omega)$ is the constant of integration (a function of $\omega$ since the ODE was at fixed $\omega$).

Divide by $e^{\kappa\omega^2 t}$:
$$U(\omega, t) = \frac{\lambda}{\kappa\omega^2}\sqrt{\frac{2}{\pi}} + K(\omega)e^{-\kappa\omega^2 t}.$$

### I.4.6 Apply the initial condition

The IC $u(x, 0) = 0$ transforms to $U(\omega, 0) = 0$:
$$0 = \frac{\lambda}{\kappa\omega^2}\sqrt{\frac{2}{\pi}} + K(\omega) \;\Longrightarrow\; K(\omega) = -\frac{\lambda}{\kappa\omega^2}\sqrt{\frac{2}{\pi}}.$$

Substitute back:
$$U(\omega, t) = \sqrt{\frac{2}{\pi}}\,\frac{\lambda}{\kappa\omega^2}\bigl(1 - e^{-\kappa\omega^2 t}\bigr).$$

### I.4.7 Apply the inverse cosine transform

$$u(x, t) = \sqrt{\frac{2}{\pi}}\int_0^\infty U(\omega, t)\cos(\omega x) d\omega.$$

Substitute:
$$u(x, t) = \sqrt{\frac{2}{\pi}}\int_0^\infty\sqrt{\frac{2}{\pi}}\,\frac{\lambda(1 - e^{-\kappa\omega^2 t})}{\kappa\omega^2}\cos(\omega x) d\omega.$$

The two factors of $\sqrt{2/\pi}$ multiply to $2/\pi$:
$$\boxed{u(x, t) = \frac{2\lambda}{\pi}\int_0^\infty\frac{1 - e^{-\kappa\omega^2 t}}{\kappa\omega^2}\cos(\omega x) d\omega.}$$

This matches the required result. ✓

### I.4.8 Pattern to remember

The recipe for Fourier transform problems:
1. Identify the right transform based on boundary data type (sine for Dirichlet, cosine for Neumann, full Fourier for $-\infty < x < \infty$).
2. Transform the PDE — derivatives become algebraic expressions, time derivatives stay.
3. Solve the resulting ODE in time (or algebraic equation if you transform in time too).
4. Apply transformed initial conditions to fix constants.
5. Inverse transform to get the answer.

---

## I.5 Sheet 2 Q7: Steady-state heat in a semi-infinite plate with insulated edge

### I.5.1 The problem

The semi-infinite plate $0 \le x < \infty$, $0 \le y < \infty$ has steady-state heat distribution governed by
$$\frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2} = 0.$$

Boundary conditions:
- A small section of the bottom edge $0 \le x \le \ell$ is held at $T_0$, while the rest is at $0°$.
- The left edge $x = 0$ is insulated: $\partial u/\partial x|_{x=0} = 0$.
- $u \to 0$ as $y \to \infty$ (boundedness).

Show that
$$u(x, y) = \frac{T_0}{\pi}\left[\arctan\!\left(\frac{\ell + x}{y}\right) + \arctan\!\left(\frac{\ell - x}{y}\right)\right].$$

### I.5.2 Choose a transform

The boundary condition at $x = 0$ is Neumann ($\partial u/\partial x = 0$). So we use the **Fourier cosine transform in $x$**.

Define $U(\omega, y) = \mathcal{C}_x[u(x, y)]$.

### I.5.3 Transform the PDE

For $u_{xx}$: use the cosine transform of second derivative formula with $u_x(0, y) = 0$:
$$\mathcal{C}_x[u_{xx}] = -\sqrt{\frac{2}{\pi}}\,u_x(0, y) - \omega^2 U = -\omega^2 U.$$

For $u_{yy}$: trivially, $\mathcal{C}_x[u_{yy}] = U_{yy}$ since the cosine transform doesn't see $y$.

So the transformed PDE is
$$-\omega^2 U + U_{yy} = 0 \;\Longrightarrow\; U_{yy} - \omega^2 U = 0.$$

This is an ODE in $y$ (with $\omega$ as a parameter).

### I.5.4 Solve the ODE

The general solution is
$$U(\omega, y) = A(\omega)e^{-\omega y} + B(\omega)e^{\omega y}.$$

The boundedness condition $u(x, y) \to 0$ as $y \to \infty$ forces $U \to 0$ as $y \to \infty$ (the inverse transform of zero is zero). The growing exponential $e^{\omega y}$ must vanish, so $B(\omega) = 0$:
$$U(\omega, y) = A(\omega)e^{-\omega y}.$$

### I.5.5 Apply the bottom-edge condition

The condition at $y = 0$ is
$$u(x, 0) = f(x) = \begin{cases} T_0 & 0 \le x \le \ell \\ 0 & x > \ell\end{cases}$$

Transform:
$$U(\omega, 0) = \mathcal{C}_x[f(x)] = \sqrt{\frac{2}{\pi}}\int_0^\ell T_0\cos(\omega x) dx.$$

Compute:
$$\int_0^\ell\cos(\omega x) dx = \left[\frac{\sin(\omega x)}{\omega}\right]_0^\ell = \frac{\sin(\omega\ell)}{\omega}.$$

So:
$$U(\omega, 0) = \sqrt{\frac{2}{\pi}}\,T_0\,\frac{\sin(\omega\ell)}{\omega}.$$

This must equal $A(\omega)e^{0} = A(\omega)$:
$$A(\omega) = \sqrt{\frac{2}{\pi}}\,T_0\,\frac{\sin(\omega\ell)}{\omega}.$$

So:
$$U(\omega, y) = \sqrt{\frac{2}{\pi}}\,\frac{T_0\sin(\omega\ell)}{\omega}\,e^{-\omega y}.$$

### I.5.6 Apply the inverse cosine transform

$$u(x, y) = \sqrt{\frac{2}{\pi}}\int_0^\infty U(\omega, y)\cos(\omega x) d\omega = \frac{2T_0}{\pi}\int_0^\infty\frac{\sin(\omega\ell)\cos(\omega x)}{\omega}e^{-\omega y} d\omega.$$

### I.5.7 Use a product-to-sum identity

To evaluate this, use the trigonometric identity
$$\sin A\cos B = \frac{1}{2}[\sin(A + B) + \sin(A - B)].$$

With $A = \omega\ell$, $B = \omega x$:
$$\sin(\omega\ell)\cos(\omega x) = \frac{1}{2}[\sin(\omega(\ell + x)) + \sin(\omega(\ell - x))].$$

Substitute:
$$u(x, y) = \frac{T_0}{\pi}\int_0^\infty\frac{e^{-\omega y}}{\omega}[\sin(\omega(\ell + x)) + \sin(\omega(\ell - x))] d\omega.$$

### I.5.8 Apply the given integral identity

The problem provides the integral
$$\int_0^\infty\frac{e^{-bx}}{x}\sin(ax) dx = \arctan\!\left(\frac{a}{b}\right).$$

Apply this twice (with the integration variable being $\omega$, $b = y$, and $a$ being $\ell+x$ or $\ell-x$):
$$\int_0^\infty\frac{e^{-\omega y}}{\omega}\sin(\omega(\ell + x)) d\omega = \arctan\!\left(\frac{\ell + x}{y}\right),$$
$$\int_0^\infty\frac{e^{-\omega y}}{\omega}\sin(\omega(\ell - x)) d\omega = \arctan\!\left(\frac{\ell - x}{y}\right).$$

Combine:
$$\boxed{u(x, y) = \frac{T_0}{\pi}\left[\arctan\!\left(\frac{\ell + x}{y}\right) + \arctan\!\left(\frac{\ell - x}{y}\right)\right].} \;\;\checkmark$$

### I.5.9 Sanity checks

- At $y \to \infty$: each $\arctan$ argument goes to $0$, so $u \to 0$. ✓
- At $y = 0^+$:
  - For $0 < x < \ell$: $(\ell + x)/y \to +\infty$ and $(\ell - x)/y \to +\infty$, so each arctan $\to \pi/2$. Sum $= \pi$. $u = T_0\cdot\pi/\pi = T_0$. ✓
  - For $x > \ell$: $(\ell + x)/y \to +\infty$ but $(\ell - x)/y \to -\infty$, so first arctan $\to \pi/2$ and second $\to -\pi/2$. Sum $= 0$. $u = 0$. ✓
- At $x = 0$: $\partial u/\partial x|_{x=0} = (T_0/\pi)\bigl[\dfrac{1/y}{1 + (\ell/y)^2} + \dfrac{-1/y}{1 + (\ell/y)^2}\bigr] = 0$. ✓ (insulated edge)

---

# Part J — The Full Fourier Transform

## J.1 Definition and key properties

The full Fourier transform (with the course's conventions):
$$U(k) = \mathcal{F}[u](k) = \frac{1}{\sqrt{2\pi}}\int_{-\infty}^\infty u(x) e^{-ikx} dx.$$
$$u(x) = \mathcal{F}^{-1}[U](x) = \frac{1}{\sqrt{2\pi}}\int_{-\infty}^\infty U(k) e^{ikx} dk.$$

Use it for problems on the *infinite* domain $-\infty < x < \infty$ (no boundary at $x = 0$).

### J.1.1 Key properties (memorise these)

- **Derivative:** $\mathcal{F}[\partial u/\partial x] = ik\,U(k)$.
- **Higher derivatives:** $\mathcal{F}[\partial^n u/\partial x^n] = (ik)^n U(k)$. In particular $\mathcal{F}[u_{xx}] = -k^2 U$.
- **Delta:** $\mathcal{F}[\delta(x - x_0)] = e^{-ikx_0}/\sqrt{2\pi}$.
- **Convolution:** $\mathcal{F}[f \otimes g] = \sqrt{2\pi}\,F(k)G(k)$, where $(f\otimes g)(x) = \int f(u)g(x - u) du$.
- **Multiplication:** $\mathcal{F}[fg] = (1/\sqrt{2\pi})\,F\otimes G$.
- **Gaussian:** $\mathcal{F}[e^{-x^2/(2\sigma^2)}] = \sigma\,e^{-\sigma^2 k^2/2}$ (Gaussians transform to Gaussians).

### J.1.2 Why the derivative property?

It's so useful, let's see why $\mathcal{F}[\partial u/\partial x] = ik\,U(k)$.

Start with the inverse transform $u(x) = (1/\sqrt{2\pi})\int U(k)e^{ikx} dk$. Differentiate with respect to $x$:
$$\frac{\partial u}{\partial x} = \frac{1}{\sqrt{2\pi}}\int U(k)\cdot ik\,e^{ikx} dk = \frac{1}{\sqrt{2\pi}}\int [ik\,U(k)]e^{ikx} dk.$$

This is the inverse transform of $ik\,U(k)$, so $\mathcal{F}[\partial u/\partial x] = ik\,U(k)$. ✓

This is the essence of why Fourier transforms simplify PDEs: derivatives become multiplications.

---

## J.2 Sheet 2 Q8: Transform of various PDEs

We just apply the derivative property term by term.

### J.2.1 Part (a): $\partial^n u/\partial x^n = 0$ (transform w.r.t. $x$)

$$\mathcal{F}[\partial^n u/\partial x^n] = (ik)^n U(k) = 0.$$

### J.2.2 Part (b): $u_{xx} + u_{xy} - 5u_y = 0$ (transform w.r.t. $x$ and $y$)

Each spatial derivative becomes multiplication by the corresponding $i$-times-wavenumber:
- $\partial/\partial x \to ik_x$.
- $\partial/\partial y \to ik_y$.

So:
- $u_{xx} \to (ik_x)^2 U = -k_x^2 U$.
- $u_{xy} \to (ik_x)(ik_y) U = -k_x k_y U$.
- $u_y \to ik_y U$.

Substitute:
$$-k_x^2 U - k_x k_y U - 5ik_y U = 0,$$
or factoring:
$$\bigl(-k_x^2 - k_x k_y - 5ik_y\bigr)U(k_x, k_y) = 0.$$

### J.2.3 Part (c): $u_{xx} + (1/v^2)u_{tt} = 0$ (transform w.r.t. $x$ only, *not* $t$)

Since we only transform in $x$:
- $u_{xx} \to -k^2 U(k, t)$.
- $u_{tt}$: the cosine and sine transforms of derivatives in $t$ remain $\partial^2 U/\partial t^2$ (since $t$ is being treated as a parameter, not transformed).

So:
$$-k^2 U + \frac{1}{v^2}\frac{\partial^2 U}{\partial t^2} = 0.$$

### J.2.4 Part (d): same PDE, transform w.r.t. $x$ *and* $t$

Now $t \to \omega$:
- $u_{xx} \to -k^2 U(k, \omega)$.
- $u_{tt} \to (i\omega)^2 U = -\omega^2 U$.

Substitute:
$$-k^2 U - \frac{\omega^2}{v^2}U = 0 \;\Longrightarrow\; \left(k^2 + \frac{\omega^2}{v^2}\right)U(k, \omega) = 0.$$

For real $k$ and $\omega$, this implies $U=0$ in the ordinary full-Fourier-transform sense. This is not the usual wave equation; the usual wave equation would be $u_{xx} - v^{-2}u_{tt}=0$, which would transform to $(-k^2 + \omega^2/v^2)U=0$ and give the dispersion relation $\omega=\pm vk$. So the plus sign in $u_{xx}+v^{-2}u_{tt}=0$ makes this elliptic rather than hyperbolic.

### J.2.5 Part (e): Free Schrödinger $-\dfrac{\hbar^2}{2m}u_{xx} = i\hbar u_t$ (transform w.r.t. $x$ and $t$)

- $u_{xx} \to -k^2 U(k, \omega)$.
- $u_t \to i\omega U$.

Substitute:
$$-\frac{\hbar^2}{2m}(-k^2 U) = i\hbar(i\omega U) \;\Longrightarrow\; \frac{\hbar^2 k^2}{2m}U = -\hbar\omega U.$$

With the transform convention used here, this gives:
$$\omega = -\frac{\hbar k^2}{2m}.$$

**Sign-convention warning:** in the usual physical plane wave convention $u\sim e^{i(kx-\Omega t)}$, the physical angular frequency is positive,
$$\Omega = \frac{\hbar k^2}{2m}.$$
The negative sign above comes from the particular full Fourier transform convention, not from negative kinetic energy. The physical energy remains $E=\hbar\Omega=\hbar^2k^2/(2m)=p^2/(2m)$.

### J.2.6 Part (f): Schrödinger with potential, $-\dfrac{\hbar^2}{2m}u_{xx} + V(x)u = i\hbar u_t$

The new feature: the term $V(x)\,u(x, t)$ is a *product* of two functions of $x$. Its Fourier transform is a *convolution*.

Using the multiplication property $\mathcal{F}[V u] = (1/\sqrt{2\pi})\,V \otimes U$ where $V(k) = \mathcal{F}[V(x)]$:
$$\mathcal{F}_x[V(x)u(x, t)] = \frac{1}{\sqrt{2\pi}}\int_{-\infty}^\infty V(k')U(k - k', \omega) dk'.$$

So the transformed equation is:
$$\frac{\hbar^2 k^2}{2m}U(k, \omega) + \frac{1}{\sqrt{2\pi}}\int_{-\infty}^\infty V(k')U(k - k', \omega) dk' = -\hbar\omega U(k, \omega).$$

This is an *integral* equation in $k$ — generally hard to solve, but useful for perturbation theory.

### J.2.7 Part (g): $\nabla\cdot\mathbf{u} = 0$ (transform w.r.t. $x, y, z$)

Expanded: $\partial_x u_x + \partial_y u_y + \partial_z u_z = 0$. With $\mathbf{k} = (k_x, k_y, k_z)$ and $\mathbf{U} = (U_x, U_y, U_z)$:
$$ik_x U_x + ik_y U_y + ik_z U_z = 0.$$
Or:
$$i\mathbf{k}\cdot\mathbf{U}(\mathbf{k}) = 0 \;\Longleftrightarrow\; \mathbf{k}\cdot\mathbf{U} = 0.$$

So divergence-free vector fields have transforms perpendicular to $\mathbf{k}$.

### J.2.8 Part (h): $\nabla\times\mathbf{u} = 0$

Similarly, the curl operator $\nabla\times$ becomes multiplication by $i\mathbf{k}\times$:
$$i\mathbf{k}\times\mathbf{U}(\mathbf{k}) = \mathbf{0} \;\Longleftrightarrow\; \mathbf{k}\times\mathbf{U} = \mathbf{0}.$$

So curl-free fields have transforms parallel to $\mathbf{k}$.

These last two results (g, h) together form the basis of the **Helmholtz decomposition**: any vector field can be split into a divergence-free part (transverse, $\mathbf{k}\perp\mathbf{U}$) and a curl-free part (longitudinal, $\mathbf{k}\parallel\mathbf{U}$). In Fourier space this is just splitting a vector into its components perpendicular and parallel to $\mathbf{k}$.

---

## J.3 Sheet 2 Q9: Water vapour over a lake (steady-state diffusion)

### J.3.1 The problem

Water vapour above a lake reaches steady state. We model in 2D with $u(x, z)$ the concentration at horizontal position $x$ and height $z$ above the lake surface.

(a) Write down the PDE. (b) Take the Fourier transform with respect to $x$. (c) Show
$$u(x, z) = \frac{1}{\pi}\int_{-\infty}^\infty\frac{z\,c(s)}{z^2 + (s - x)^2} ds$$
given $u(x, 0) = c(x)$. (d) Find $u(x, z)$ if $c(x) = c_0$ for $-a \le x \le a$ and $0$ outside.

### J.3.2 Part (a) — The PDE

In steady state with diffusion alone (no advection, no sources), the concentration satisfies **Laplace's equation**:
$$\frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial z^2} = 0.$$

(This is the same structure as steady-state heat conduction.)

### J.3.3 Part (b) — Transform w.r.t. $x$

The horizontal extent is infinite, $-\infty < x < \infty$, so the full Fourier transform in $x$ is appropriate. Let $U(k, z) = \mathcal{F}_x[u(x, z)]$.

Applying the derivative property:
- $u_{xx} \to -k^2 U(k, z)$.
- $u_{zz} \to U_{zz}(k, z)$ (no transform in $z$).

The PDE becomes
$$-k^2 U + U_{zz} = 0 \;\Longrightarrow\; U_{zz} - k^2 U = 0.$$

This is an ODE in $z$ (with $k$ as a parameter).

### J.3.4 Part (c) — Solve and apply boundary conditions

The general solution to $U_{zz} = k^2 U$ is:
$$U(k, z) = A(k)e^{-|k|z} + B(k)e^{|k|z}.$$

(I write $|k|$ instead of $k$ to ensure exponential decay for both signs of $k$. Some texts write $\sqrt{k^2}$ or just $|k|$ — these are the same.)

**Boundedness:** As $z \to \infty$, $u$ should remain finite (the vapour concentration shouldn't diverge at infinite height). This kills the growing exponential: $B(k) = 0$.
$$U(k, z) = A(k)e^{-|k|z}.$$

**Surface boundary:** At $z = 0$, we have $u(x, 0) = c(x)$. Transform: $U(k, 0) = C(k) = \mathcal{F}_x[c(x)]$.

So $A(k) = C(k)$:
$$U(k, z) = C(k)e^{-|k|z}.$$

**Inverse transform:**
$$u(x, z) = \frac{1}{\sqrt{2\pi}}\int_{-\infty}^\infty C(k) e^{-|k|z} e^{ikx} dk.$$

Substitute the definition $C(k) = (1/\sqrt{2\pi})\int c(s) e^{-iks} ds$:
$$u(x, z) = \frac{1}{2\pi}\int_{-\infty}^\infty\int_{-\infty}^\infty c(s)e^{-iks}\,e^{-|k|z}\,e^{ikx} ds\, dk.$$

Swap the order of integration:
$$u(x, z) = \frac{1}{2\pi}\int_{-\infty}^\infty c(s)\left[\int_{-\infty}^\infty e^{-|k|z + ik(x - s)} dk\right] ds.$$

### J.3.5 Evaluate the inner integral

Compute
$$I(x - s, z) = \int_{-\infty}^\infty e^{-|k|z + ik(x - s)} dk.$$

Split into negative and positive $k$:
$$I = \int_{-\infty}^0 e^{kz}e^{ik(x-s)} dk + \int_0^\infty e^{-kz}e^{ik(x-s)} dk.$$

(For $k < 0$, $|k| = -k$, so $e^{-|k|z} = e^{kz}$.)

For the second integral:
$$\int_0^\infty e^{-kz + ik(x-s)} dk = \int_0^\infty e^{k[i(x-s) - z]} dk = \frac{1}{z - i(x-s)}.$$

For the first integral, substitute $k' = -k$ (so $dk = -dk'$, limits flip):
$$\int_{-\infty}^0 e^{kz + ik(x-s)} dk = \int_0^\infty e^{-k'z - ik'(x-s)} dk' = \frac{1}{z + i(x-s)}.$$

Add:
$$I = \frac{1}{z + i(x-s)} + \frac{1}{z - i(x-s)} = \frac{[z - i(x-s)] + [z + i(x-s)]}{[z + i(x-s)][z - i(x-s)]} = \frac{2z}{z^2 + (x-s)^2}.$$

### J.3.6 Combine

Substitute the inner integral back:
$$u(x, z) = \frac{1}{2\pi}\int_{-\infty}^\infty c(s)\cdot\frac{2z}{z^2 + (x-s)^2} ds = \frac{1}{\pi}\int_{-\infty}^\infty\frac{z\,c(s)}{z^2 + (s - x)^2} ds.$$

(Note that $(x-s)^2 = (s-x)^2$, so the form matches the problem statement.)

$$\boxed{u(x, z) = \frac{1}{\pi}\int_{-\infty}^\infty\frac{z\,c(s)}{z^2 + (s - x)^2} ds.}\;\;\checkmark$$

This is the **Poisson integral formula** for the upper half-plane — a classical result in potential theory. The kernel $\dfrac{z/\pi}{z^2 + (s-x)^2}$ is a Lorentzian peaked at $s = x$ with half-width $z$. Physically: the value of $u$ at height $z$ above the surface is a Lorentzian-weighted average of the surface values, with the weighting becoming more localised as $z \to 0$ (which makes sense — close to the surface, you mostly feel the local value).

### J.3.7 Part (d) — Evaluate for a top-hat surface concentration

Now apply the Poisson formula with $c(s) = c_0$ for $-a \le s \le a$ and $c(s) = 0$ outside:
$$u(x, z) = \frac{c_0}{\pi}\int_{-a}^a\frac{z}{z^2 + (s-x)^2} ds.$$

**Substitution:** Let $w = (s - x)/z$, so $dw = ds/z$, hence $ds = z\,dw$.

When $s = -a$: $w = (-a - x)/z$. When $s = a$: $w = (a - x)/z$.

$$u(x, z) = \frac{c_0}{\pi}\int_{(-a-x)/z}^{(a-x)/z}\frac{z}{z^2(1 + w^2)} z\,dw = \frac{c_0}{\pi}\int_{(-a-x)/z}^{(a-x)/z}\frac{1}{1 + w^2} dw.$$

The integrand is the standard $\arctan$ derivative:
$$u(x, z) = \frac{c_0}{\pi}\bigl[\arctan w\bigr]_{(-a-x)/z}^{(a-x)/z} = \frac{c_0}{\pi}\left[\arctan\!\left(\frac{a-x}{z}\right) - \arctan\!\left(\frac{-a-x}{z}\right)\right].$$

Use $\arctan(-y) = -\arctan(y)$:
$$u(x, z) = \frac{c_0}{\pi}\left[\arctan\!\left(\frac{a-x}{z}\right) + \arctan\!\left(\frac{a+x}{z}\right)\right].$$

$$\boxed{u(x, z) = \frac{c_0}{\pi}\left[\arctan\!\left(\frac{a-x}{z}\right) + \arctan\!\left(\frac{a+x}{z}\right)\right].}$$

### J.3.8 Sanity checks

- **At surface** ($z \to 0$):
  - For $|x| < a$: $(a-x)/z, (a+x)/z \to +\infty$, so each arctan $\to \pi/2$, sum $= \pi$. $u = c_0$. ✓
  - For $|x| > a$ (say $x > a$): $(a - x)/z \to -\infty$, $(a + x)/z \to +\infty$, so first arctan $\to -\pi/2$, second $\to +\pi/2$. Sum $= 0$. $u = 0$. ✓
- **High up** ($z \to \infty$): both arctan arguments $\to 0$, so $u \to 0$. ✓
- This formula is identical in structure to Sheet 2 Q7 (insulated semi-infinite plate), reflecting that they are different statements of the same boundary-value problem for Laplace's equation in a half-plane.

---

# Part K — Green's Functions

## K.1 Sheet 2 Q10: What is a Green's function?

### K.1.1 The problem

What is a Green's function? How are they useful for solving PDEs?

### K.1.2 The defining idea

Imagine you have a linear PDE $\mathcal{L}u = f$ where $\mathcal{L}$ is some linear differential operator (like $\nabla^2$, or $\partial_t - \kappa\nabla^2$, or $\partial_t^2 - c^2\nabla^2$) and $f$ is some source term.

The **Green's function** $G(\mathbf{r}, \mathbf{r}')$ is defined as the response of the system to a point source. Specifically:
$$\mathcal{L}_\mathbf{r} G(\mathbf{r}, \mathbf{r}') = \delta(\mathbf{r} - \mathbf{r}'),$$
where the subscript $\mathbf{r}$ on $\mathcal{L}$ means the operator acts on the $\mathbf{r}$ argument (treating $\mathbf{r}'$ as a parameter — the location of the point source).

In words: $G$ is what you get from the system at the **field point** $\mathbf{r}$ when you place a unit point source at the **source point** $\mathbf{r}'$.

### K.1.3 Why is this useful?

It's all about **superposition** — the principle that, for linear PDEs, a solution can be built from a sum (or integral) of simpler solutions.

A general source $f(\mathbf{r}')$ can be decomposed as a continuous superposition of delta-function sources, using the sifting property:
$$f(\mathbf{r}) = \int f(\mathbf{r}')\delta(\mathbf{r} - \mathbf{r}') d\mathbf{r}'.$$

Each delta source produces a response $G$. The total response (linear combination = integral) is:
$$u(\mathbf{r}) = \int G(\mathbf{r}, \mathbf{r}')f(\mathbf{r}') d\mathbf{r}'.$$

This is the **particular solution** to $\mathcal{L}u = f$. The general solution adds a complementary solution to the homogeneous problem $\mathcal{L}u_c = 0$.

### K.1.4 Verifying that this works

Apply $\mathcal{L}$ to both sides:
$$\mathcal{L}u(\mathbf{r}) = \mathcal{L}\int G(\mathbf{r}, \mathbf{r}')f(\mathbf{r}') d\mathbf{r}'.$$

Pull $\mathcal{L}$ inside the integral (it acts on $\mathbf{r}$, while the integration is over $\mathbf{r}'$):
$$\mathcal{L}u = \int \mathcal{L}_\mathbf{r} G(\mathbf{r}, \mathbf{r}')\cdot f(\mathbf{r}') d\mathbf{r}' = \int\delta(\mathbf{r} - \mathbf{r}')f(\mathbf{r}') d\mathbf{r}' = f(\mathbf{r}). \;\checkmark$$

### K.1.5 Standard Green's functions worth knowing

**Free-space Green's function for the 3D Laplacian** ($\mathcal{L} = \nabla^2$):
$$G(\mathbf{r}, \mathbf{r}') = -\frac{1}{4\pi|\mathbf{r} - \mathbf{r}'|}.$$

This is the kernel behind:
- Coulomb's law: potential of a point charge $Q$ at $\mathbf{r}'$ is $V = Q/(4\pi\varepsilon_0|\mathbf{r} - \mathbf{r}'|)$.
- Newton's gravitation: gravitational potential of a point mass $M$ is $V = -GM/|\mathbf{r} - \mathbf{r}'|$.

**Free-space Green's function for the 3D Helmholtz equation** depends on the source-sign convention. With the convention used above,
$$\mathcal L G = \delta, \qquad \mathcal L=\nabla^2+k^2,$$
the free-space Green's function is
$$G(\mathbf{r}, \mathbf{r}') = -\frac{e^{\pm ik|\mathbf{r} - \mathbf{r}'|}}{4\pi|\mathbf{r} - \mathbf{r}'|}.$$

Many physics texts instead define $(\nabla^2+k^2)G=-\delta$, in which case the sign is positive. The $+$ or $-$ in the exponential selects outgoing or incoming spherical waves, depending on the time-dependence convention.

### K.1.6 Boundaries and the method of images

Free-space Green's functions assume no boundaries. If your problem has boundaries (e.g. a grounded plate, a fixed-end string), the Green's function must satisfy the homogeneous boundary conditions there.

The **method of images** constructs such Green's functions by placing fictitious "image" sources outside the physical domain such that the combined potential satisfies the boundary conditions. The uniqueness theorem then guarantees correctness inside the physical region.

Example: For a point charge at distance $z'$ above an infinite grounded plate at $z = 0$, the image is an opposite-sign charge at $-z'$, mirrored through the plate. The corrected Green's function is:
$$G_\text{plate}(\mathbf{r}, \mathbf{r}') = -\frac{1}{4\pi}\left[\frac{1}{|\mathbf{r} - \mathbf{r}'|} - \frac{1}{|\mathbf{r} - \mathbf{r}'_\text{image}|}\right],$$
where $\mathbf{r}'_\text{image}$ is the mirror image of $\mathbf{r}'$.

---

## K.2 Sheet 2 Q11: Struck string at the midpoint

### K.2.1 The problem

A string of length $\ell$ is fixed at both ends and initially at rest. It is struck at its midpoint $x = \ell/2$, imparting momentum $p$. The initial conditions are:
- $u(x, 0) = 0$ (initially at rest in position).
- The initial velocity is concentrated near the midpoint:
$$\frac{\partial u}{\partial t}\bigg|_{t=0} = \begin{cases} 0, & 0 < x < \ell/2 - \delta \\ v_0, & \ell/2 - \delta < x < \ell/2 + \delta \\ 0, & \ell/2 + \delta < x < \ell\end{cases}$$
with $v_0 = p/(2\delta\rho)$ (where $\rho$ is the linear mass density).

Determine the motion. Then take the limit $\delta \to 0$ (an idealised point strike).

### K.2.2 Why $v_0 = p/(2\delta\rho)$?

A small region of length $2\delta$ has mass $2\delta\rho$. Total momentum imparted is mass times velocity: $(2\delta\rho)(v_0) = p$, so $v_0 = p/(2\delta\rho)$. The product $v_0\cdot 2\delta = p/\rho$ remains finite even as $\delta \to 0$ — physically, the impulse is well-defined even for a point strike.

### K.2.3 Use the "struck from rest" framework

Wave equation $u_{tt} = c^2 u_{xx}$ with $c = \sqrt{T/\rho}$ ($T$ = tension). Fixed ends → $\sin(n\pi x/\ell)$ in space. Zero initial displacement → only $\sin(n\pi c t/\ell)$ in time:
$$u(x, t) = \sum_{n=1}^\infty B_n\sin\!\left(\frac{n\pi x}{\ell}\right)\sin\!\left(\frac{n\pi c t}{\ell}\right).$$

### K.2.4 Apply the initial velocity condition

Differentiate w.r.t. $t$:
$$\frac{\partial u}{\partial t} = \sum_{n=1}^\infty B_n\cdot\frac{n\pi c}{\ell}\sin\!\left(\frac{n\pi x}{\ell}\right)\cos\!\left(\frac{n\pi c t}{\ell}\right).$$

At $t = 0$:
$$\frac{\partial u}{\partial t}\bigg|_{t=0} = \sum_{n=1}^\infty\underbrace{\frac{n\pi c}{\ell}B_n}_{=:A_n}\sin\!\left(\frac{n\pi x}{\ell}\right) = g(x).$$

So $A_n = (n\pi c/\ell) B_n$ are the Fourier sine coefficients of $g(x)$:
$$A_n = \frac{2}{\ell}\int_0^\ell g(x)\sin\!\left(\frac{n\pi x}{\ell}\right) dx.$$

### K.2.5 Compute $A_n$

Since $g(x) = v_0$ only on $[\ell/2 - \delta, \ell/2 + \delta]$:
$$A_n = \frac{2v_0}{\ell}\int_{\ell/2 - \delta}^{\ell/2 + \delta}\sin\!\left(\frac{n\pi x}{\ell}\right) dx.$$

Compute the integral:
$$\int_{\ell/2 - \delta}^{\ell/2 + \delta}\sin\!\left(\frac{n\pi x}{\ell}\right) dx = \left[-\frac{\ell}{n\pi}\cos\!\left(\frac{n\pi x}{\ell}\right)\right]_{\ell/2 - \delta}^{\ell/2 + \delta}.$$

$$= -\frac{\ell}{n\pi}\left[\cos\!\left(\frac{n\pi}{2} + \frac{n\pi\delta}{\ell}\right) - \cos\!\left(\frac{n\pi}{2} - \frac{n\pi\delta}{\ell}\right)\right].$$

### K.2.6 Apply the sum-to-product identity

Use $\cos(A + B) - \cos(A - B) = -2\sin A\sin B$. With $A = n\pi/2$, $B = n\pi\delta/\ell$:
$$\cos\!\left(\frac{n\pi}{2} + \frac{n\pi\delta}{\ell}\right) - \cos\!\left(\frac{n\pi}{2} - \frac{n\pi\delta}{\ell}\right) = -2\sin\!\left(\frac{n\pi}{2}\right)\sin\!\left(\frac{n\pi\delta}{\ell}\right).$$

So:
$$\int = -\frac{\ell}{n\pi}\cdot\left[-2\sin\!\left(\frac{n\pi}{2}\right)\sin\!\left(\frac{n\pi\delta}{\ell}\right)\right] = \frac{2\ell}{n\pi}\sin\!\left(\frac{n\pi}{2}\right)\sin\!\left(\frac{n\pi\delta}{\ell}\right).$$

Multiply by $2v_0/\ell$:
$$A_n = \frac{2v_0}{\ell}\cdot\frac{2\ell}{n\pi}\sin\!\left(\frac{n\pi}{2}\right)\sin\!\left(\frac{n\pi\delta}{\ell}\right) = \frac{4v_0}{n\pi}\sin\!\left(\frac{n\pi}{2}\right)\sin\!\left(\frac{n\pi\delta}{\ell}\right).$$

Substitute $v_0 = p/(2\delta\rho)$:
$$A_n = \frac{4}{n\pi}\cdot\frac{p}{2\delta\rho}\sin\!\left(\frac{n\pi}{2}\right)\sin\!\left(\frac{n\pi\delta}{\ell}\right) = \frac{2p}{n\pi\rho\delta}\sin\!\left(\frac{n\pi}{2}\right)\sin\!\left(\frac{n\pi\delta}{\ell}\right).$$

### K.2.7 Take the point-strike limit $\delta \to 0$

The factor $\sin(n\pi\delta/\ell)/\delta$ has a finite limit. Using the small-angle approximation $\sin(x) \approx x$:
$$\lim_{\delta \to 0}\frac{\sin(n\pi\delta/\ell)}{\delta} = \frac{n\pi}{\ell}.$$

So:
$$\lim_{\delta\to 0}A_n = \frac{2p}{n\pi\rho}\sin\!\left(\frac{n\pi}{2}\right)\cdot\frac{n\pi}{\ell} = \frac{2p}{\rho\ell}\sin\!\left(\frac{n\pi}{2}\right).$$

### K.2.8 Recover $B_n$

Since $A_n = (n\pi c/\ell) B_n$:
$$B_n = \frac{\ell}{n\pi c}A_n = \frac{\ell}{n\pi c}\cdot\frac{2p}{\rho\ell}\sin\!\left(\frac{n\pi}{2}\right) = \frac{2p}{n\pi\rho c}\sin\!\left(\frac{n\pi}{2}\right).$$

### K.2.9 Final solution

$$\boxed{u(x, t) = \sum_{n=1}^\infty\frac{2p}{n\pi\rho c}\sin\!\left(\frac{n\pi}{2}\right)\sin\!\left(\frac{n\pi x}{\ell}\right)\sin\!\left(\frac{n\pi c t}{\ell}\right).}$$

### K.2.10 Physical insight: which modes ring?

The factor $\sin(n\pi/2)$:
- $n = 1$: $\sin(\pi/2) = 1$. ✓
- $n = 2$: $\sin(\pi) = 0$. ✗
- $n = 3$: $\sin(3\pi/2) = -1$. ✓
- $n = 4$: $\sin(2\pi) = 0$. ✗
- ...

So only **odd harmonics** are excited, with alternating signs: $1, -1, 1, -1, \ldots$

**Why?** The even modes ($n = 2, 4, 6, \ldots$) all have a *node* at $x = \ell/2$ — they don't move at the midpoint. A strike at the midpoint cannot excite a mode that doesn't move there. Only modes with antinodes at $\ell/2$ ring.

This is the same physical principle used by guitarists: pluck a string near the bridge to favour high harmonics, or near the centre to favour the fundamental.

---

## K.3 Sheet 2 Q12: Electrostatic potential of a thin charged glass rod

### K.3.1 The problem

A thin glass rod of length $L = 10$ cm carries a total triboelectric (rubbing-induced) charge $Q = 8\times 10^{-10}$ C, distributed uniformly. Write down the differential equation for the electrostatic potential $V(\mathbf{r})$ and find $V$ assuming $V \to 0$ at infinity.

### K.3.2 The governing PDE

Electrostatic potential in vacuum satisfies **Poisson's equation**:
$$\nabla^2 V(\mathbf{r}) = -\frac{\rho_e(\mathbf{r})}{\varepsilon_0},$$
where $\rho_e$ is the volume charge density and $\varepsilon_0$ is the vacuum permittivity.

### K.3.3 Express the charge distribution

Place the rod along the $z$-axis, centred at the origin, from $z = -L/2$ to $z = L/2$. The rod is "thin" → treat as a 1D line charge. The linear charge density is
$$\lambda = Q/L \;\;(\text{constant, since uniform}).$$

In 3D, a line charge along the $z$-axis can be written as a volume charge density using delta functions for the transverse directions:
$$\rho_e(\mathbf{r}) = \lambda\,\delta(x)\,\delta(y) \cdot \chi_{[-L/2, L/2]}(z),$$
where $\chi$ is 1 on the support and 0 outside.

### K.3.4 Use the free-space Green's function

The free-space Green's function for $\nabla^2$ is $G(\mathbf{r}, \mathbf{r}') = -1/(4\pi|\mathbf{r} - \mathbf{r}'|)$. With Poisson's equation $\nabla^2 V = -\rho_e/\varepsilon_0$, the source term is $f = -\rho_e/\varepsilon_0$, so the particular solution (with $V \to 0$ at infinity) is
$$V(\mathbf{r}) = \int G(\mathbf{r}, \mathbf{r}')\cdot\left(-\frac{\rho_e(\mathbf{r}')}{\varepsilon_0}\right) d\mathbf{r}'$$
$$= \int\left(-\frac{1}{4\pi|\mathbf{r} - \mathbf{r}'|}\right)\cdot\left(-\frac{\rho_e(\mathbf{r}')}{\varepsilon_0}\right) d\mathbf{r}' = \frac{1}{4\pi\varepsilon_0}\int\frac{\rho_e(\mathbf{r}')}{|\mathbf{r} - \mathbf{r}'|} d\mathbf{r}'.$$

This is exactly Coulomb's law for a continuous charge distribution.

### K.3.5 Apply to the rod

Substitute the charge density. The $\delta(x')\delta(y')$ factors collapse the $x'$ and $y'$ integrals via the sifting property, leaving only the $z'$ integral over the rod's length:
$$V(\mathbf{r}) = \frac{\lambda}{4\pi\varepsilon_0}\int_{-L/2}^{L/2}\frac{dz'}{\sqrt{(x - 0)^2 + (y - 0)^2 + (z - z')^2}}.$$

Define the cylindrical radius $s = \sqrt{x^2 + y^2}$ — the perpendicular distance from the rod's axis. Then:
$$V(s, z) = \frac{\lambda}{4\pi\varepsilon_0}\int_{-L/2}^{L/2}\frac{dz'}{\sqrt{s^2 + (z - z')^2}}.$$

### K.3.6 Evaluate the integral

Substitute $u = z - z'$, so $du = -dz'$:
- When $z' = -L/2$: $u = z + L/2$.
- When $z' = L/2$: $u = z - L/2$.

$$\int_{-L/2}^{L/2}\frac{dz'}{\sqrt{s^2 + (z-z')^2}} = -\int_{z + L/2}^{z - L/2}\frac{du}{\sqrt{s^2 + u^2}} = \int_{z - L/2}^{z + L/2}\frac{du}{\sqrt{s^2 + u^2}}.$$

The integral $\int\frac{du}{\sqrt{s^2 + u^2}}$ is a standard form: $\sinh^{-1}(u/s)$, or equivalently $\ln\bigl(u + \sqrt{s^2 + u^2}\bigr)$ (up to a constant).

So:
$$V(s, z) = \frac{\lambda}{4\pi\varepsilon_0}\Bigl[\ln(u + \sqrt{s^2 + u^2})\Bigr]_{u = z - L/2}^{u = z + L/2}.$$

Substituting $\lambda = Q/L$:
$$\boxed{V(s, z) = \frac{Q}{4\pi\varepsilon_0 L}\,\ln\!\left[\frac{(z + L/2) + \sqrt{s^2 + (z + L/2)^2}}{(z - L/2) + \sqrt{s^2 + (z - L/2)^2}}\right].}$$

### K.3.7 Sanity checks

**Far-field limit** ($r = \sqrt{s^2 + z^2} \gg L$). For large $r$, both square roots become approximately $r$, so the argument of the log is $(r + L/2)/(r - L/2) \approx 1 + L/r$. Then $\ln(1 + L/r) \approx L/r$, giving
$$V \approx \frac{Q}{4\pi\varepsilon_0 L}\cdot\frac{L}{r} = \frac{Q}{4\pi\varepsilon_0 r},$$
the point-charge formula. ✓

**On the perpendicular bisector** ($z = 0$, $s$ general):
$$V(s, 0) = \frac{Q}{4\pi\varepsilon_0 L}\ln\!\left[\frac{L/2 + \sqrt{s^2 + L^2/4}}{-L/2 + \sqrt{s^2 + L^2/4}}\right].$$
This is the well-known textbook formula for the potential of a uniformly charged finite line on its perpendicular bisector. ✓

---

# Part L — A Synthesis: Recognising Patterns

This is the most important page of the guide for exam preparation. When you see a PDE problem, work through this checklist:

## L.1 First, classify the PDE

1. **Order?** (1st, 2nd, 3rd?) — only 2nd-order linear PDEs have the elliptic/parabolic/hyperbolic classification.
2. **Linear or non-linear?** — if non-linear, expect numerical methods or special tricks.
3. **Homogeneous or inhomogeneous?** — if inhomogeneous boundary or source, may need the steady-state-plus-transient trick or a Green's function.
4. **Type?** — compute $B^2 - 4AC$.
5. **Physical context?** — equilibrium (Laplace), diffusion (heat), waves, quantum mechanics, etc.

## L.2 What conditions are given?

- **Domain shape?** Rectangle, semi-infinite strip, full plane, half-plane, disk, sphere?
- **Boundary types?** Dirichlet (value given), Neumann (derivative given), Robin (combination), Cauchy (both)?
- **Initial conditions?** None (steady state), one (heat), two (wave)?

## L.3 Choose a method

| If you see... | Try this method |
|---|---|
| Bounded domain + homogeneous BCs (or one BC after transformation) | **Separation of variables** with Fourier series. |
| Inhomogeneous BCs $T_1, T_2$ | Subtract steady state $u_{eq}$, solve homogeneous problem for the transient. |
| Domain $-\infty < x < \infty$ | **Full Fourier transform** in $x$. |
| Half-line $0 \le x < \infty$, Dirichlet at $x = 0$ | **Fourier sine transform**. |
| Half-line $0 \le x < \infty$, Neumann at $x = 0$ | **Fourier cosine transform**. |
| Wave equation on infinite domain | **D'Alembert** $u = f(x - vt) + g(x + vt)$. |
| Inhomogeneous PDE $\mathcal{L}u = f$ in free space | **Green's function method**. |
| Boundaries with high symmetry | **Method of images** to construct boundary-respecting Green's function. |

## L.4 The standard recipes

### L.4.1 Separation of variables
1. Try $u = X(x) Y(y) \cdots$.
2. Substitute, divide by $XY\cdots$, separate variables.
3. Choose separation constant sign based on which direction has bounded oscillatory solutions.
4. Solve resulting ODEs (sines/cosines or exponentials).
5. Apply homogeneous BCs to find allowed eigenvalues (quantisation: $k = n\pi/L$).
6. Apply remaining BC via Fourier series.
7. Compute Fourier coefficients via $b_n = (2/L)\int_0^L f(x)\sin(n\pi x/L) dx$ (or cosine analogue).

### L.4.2 Integral transform
1. Choose the right transform based on boundary data (Dirichlet → sine, Neumann → cosine, $-\infty < x < \infty$ → full Fourier).
2. Transform the PDE: derivatives become algebraic factors of $ik$ (or sines/cosines of $\omega$).
3. The PDE reduces to an ODE (in time, or another spatial variable) — sometimes purely algebraic.
4. Solve the ODE using the integrating factor / characteristic equation method.
5. Apply transformed initial/boundary conditions to fix constants.
6. Inverse transform to get $u$.

### L.4.3 Green's function method
1. Solve $\mathcal{L}G = \delta(\mathbf{r} - \mathbf{r}')$ with the homogeneous boundary conditions.
2. Particular solution: $u_p(\mathbf{r}) = \int G(\mathbf{r}, \mathbf{r}')f(\mathbf{r}') d\mathbf{r}'$.
3. Add complementary solution $u_c$ if needed.

## L.5 The standard integrals you will need

$$\int_0^L\sin\!\left(\frac{n\pi x}{L}\right) dx = \frac{L}{n\pi}[1 - (-1)^n] = \begin{cases} 2L/(n\pi), & n \text{ odd} \\ 0, & n \text{ even}\end{cases}$$

$$\int_0^L\sin^2\!\left(\frac{n\pi x}{L}\right) dx = \frac{L}{2}.$$

$$\int_0^L x\sin\!\left(\frac{n\pi x}{L}\right) dx = \frac{L^2}{n\pi}(-1)^{n+1}.$$

$$\int_0^L x^2\sin\!\left(\frac{n\pi x}{L}\right) dx = \frac{L^3}{n\pi}(-1)^{n+1} - \frac{2L^3}{n^3\pi^3}[1 - (-1)^n].$$

$$\int_0^\infty\frac{e^{-bx}}{x}\sin(ax) dx = \arctan(a/b), \quad b > 0.$$

$$\int_{-\infty}^\infty e^{-|k|z + ik(x-s)} dk = \frac{2z}{z^2 + (x-s)^2}, \quad z > 0.$$

$$\int\frac{du}{\sqrt{s^2 + u^2}} = \ln(u + \sqrt{s^2 + u^2}) + C = \sinh^{-1}(u/s) + C.$$

$$\frac{1}{\sqrt{2\pi}}\int_{-\infty}^\infty e^{-k^2/(2\sigma^2)} e^{ikx} dk = \sigma e^{-\sigma^2 x^2/2}.$$

## L.6 Common trigonometric identities

$$\sin A\cos B = \tfrac12[\sin(A+B) + \sin(A-B)].$$

$$\cos A\cos B = \tfrac12[\cos(A+B) + \cos(A-B)].$$

$$\sin A\sin B = \tfrac12[\cos(A-B) - \cos(A+B)].$$

$$\cos(A+B) - \cos(A-B) = -2\sin A\sin B.$$

$$\sin(A+B) + \sin(A-B) = 2\sin A\cos B.$$

These come up *constantly* when massaging the answers from Fourier transforms into closed-form expressions.

---

*End of detailed step-by-step study guide.*


---

# Part M — Combined Theory & Formula Bank

This final section collects the key definitions, formulas, and solution patterns from the whole guide in one place. Use it as a quick revision sheet before attempting problems.

## M.1 Differential equations: core vocabulary

### ODE vs PDE

- **ODE:** equation involving ordinary derivatives of a function of one independent variable, e.g. $y'(x)$ or $y''(x)$.
- **PDE:** equation involving partial derivatives of a function of several independent variables, e.g. $u_x$, $u_t$, $u_{xx}$.

### Order

The **order** of a differential equation is the order of the highest derivative appearing. Powers do not change the order.

Example: $(u_{xx})^3+u_t=0$ is second order, not sixth order.

### Linearity

A PDE is **linear** if it can be written as
$$
\mathcal L u=f,
$$
where $\mathcal L$ is a linear differential operator and $f$ is independent of $u$.

Linear examples:
$$u_t-\kappa u_{xx}=0,$$
$$u_{xx}+u_{yy}=f(x,y).$$

Nonlinear examples:
$$u u_x+u_t=0,$$
$$(u_x)^2+u_y=0,$$
$$u_{xt}=\sinh u.$$

### Homogeneous vs inhomogeneous

For linear equations:

- **Homogeneous:** $\mathcal L u=0$.
- **Inhomogeneous:** $\mathcal L u=f$, with $f\neq0$ independent of $u$.

For nonlinear equations, it is safer to say whether there is an **external source/forcing term**.

---

## M.2 Vector differential operators

### Cartesian coordinates $(x,y,z)$

Gradient of scalar $u$:
$$
\nabla u=u_x\hat{\mathbf i}+u_y\hat{\mathbf j}+u_z\hat{\mathbf k}.
$$

Divergence of vector $\mathbf u=(u_x,u_y,u_z)$:
$$
\nabla\cdot\mathbf u=\frac{\partial u_x}{\partial x}+\frac{\partial u_y}{\partial y}+\frac{\partial u_z}{\partial z}.
$$

Laplacian of scalar $u$:
$$
\nabla^2u=u_{xx}+u_{yy}+u_{zz}.
$$

### Cylindrical coordinates $(\rho,\phi,z)$

Gradient:
$$
\nabla u=u_\rho\hat{\mathbf e}_\rho+\frac{1}{\rho}u_\phi\hat{\mathbf e}_\phi+u_z\hat{\mathbf e}_z.
$$

Divergence:
$$
\nabla\cdot\mathbf u=\frac1\rho\frac{\partial(\rho u_\rho)}{\partial\rho}+\frac1\rho\frac{\partial u_\phi}{\partial\phi}+\frac{\partial u_z}{\partial z}.
$$

Laplacian:
$$
\nabla^2u=\frac1\rho\frac{\partial}{\partial\rho}\left(\rho\frac{\partial u}{\partial\rho}\right)+\frac1{\rho^2}\frac{\partial^2u}{\partial\phi^2}+\frac{\partial^2u}{\partial z^2}.
$$

### Spherical coordinates $(r,\theta,\phi)$

Gradient:
$$
\nabla u=u_r\hat{\mathbf e}_r+\frac1r u_\theta\hat{\mathbf e}_\theta+\frac1{r\sin\theta}u_\phi\hat{\mathbf e}_\phi.
$$

Divergence:
$$
\nabla\cdot\mathbf u=\frac1{r^2}\frac{\partial(r^2u_r)}{\partial r}+\frac1{r\sin\theta}\frac{\partial(\sin\theta\,u_\theta)}{\partial\theta}+\frac1{r\sin\theta}\frac{\partial u_\phi}{\partial\phi}.
$$

Laplacian:
$$
\nabla^2u=\frac1{r^2}\frac{\partial}{\partial r}\left(r^2\frac{\partial u}{\partial r}\right)+\frac1{r^2\sin\theta}\frac{\partial}{\partial\theta}\left(\sin\theta\frac{\partial u}{\partial\theta}\right)+\frac1{r^2\sin^2\theta}\frac{\partial^2u}{\partial\phi^2}.
$$

---

## M.3 Elliptic, parabolic, and hyperbolic classification

For a second-order linear PDE in two variables,
$$
A u_{xx}+B u_{xy}+C u_{yy}+\text{lower-order terms}=0,
$$
compute
$$
\Delta=B^2-4AC.
$$

Then:

| Sign of $\Delta$ | Type | Prototype | Physical meaning |
|---|---|---|---|
| $\Delta<0$ | Elliptic | $u_{xx}+u_{yy}=0$ | equilibrium / steady state |
| $\Delta=0$ | Parabolic | $u_t=\kappa u_{xx}$ | diffusion / smoothing |
| $\Delta>0$ | Hyperbolic | $u_{tt}=c^2u_{xx}$ | waves / propagation |

---

## M.4 Boundary and initial conditions

### Initial conditions

Used for time-dependent PDEs.

- First order in time: need one initial condition, e.g. $u(x,0)=f(x)$.
- Second order in time: need two initial conditions, e.g. $u(x,0)=f(x)$ and $u_t(x,0)=g(x)$.

### Boundary conditions

- **Dirichlet:** specify the value of $u$.
  $$u=g\quad\text{on the boundary}.$$

- **Neumann:** specify normal derivative.
  $$\frac{\partial u}{\partial n}=g\quad\text{on the boundary}.$$

- **Robin:** specify a linear combination.
  $$\alpha u+\beta\frac{\partial u}{\partial n}=g.$$

- **Mixed:** different boundary parts use different types.

- **Cauchy data:** specify both $u$ and a derivative, often initial displacement and initial velocity for the wave equation.

---

## M.5 Three standard PDEs and their solution signatures

### Laplace equation

$$
\nabla^2u=0.
$$

Represents steady-state heat, electrostatics without charge, incompressible potential flow, and harmonic functions.

Common 2D form:
$$u_{xx}+u_{yy}=0.
$$

A function is **harmonic** if it satisfies Laplace's equation on its domain.

Important caveat:
$$
\ln(x^2+y^2)
$$
is harmonic only away from $(0,0)$.

### Poisson equation

$$
\nabla^2u=f.
$$

Electrostatics:
$$
\nabla^2V=-\frac{\rho_e}{\varepsilon_0}.
$$

### Diffusion / heat equation

$$u_t=D u_{xx}
$$
or in higher dimensions:
$$u_t=D\nabla^2u.
$$

Gaussian heat-kernel shape:
$$u(x,t)=\frac{A}{\sqrt t}\exp\left(-\frac{x^2}{4Dt}\right).
$$

### Wave equation

$$u_{tt}=c^2u_{xx}.
$$

D'Alembert solution on an infinite line:
$$u(x,t)=f(x-ct)+g(x+ct).
$$

Functions of $x-ct$ travel right; functions of $x+ct$ travel left.

---

## M.6 Separation of variables: standard recipe

For a PDE in $x,y$, try
$$u(x,y)=X(x)Y(y).
$$

Substitute into the PDE, divide by $XY$, and separate:
$$
\frac{X''}{X}=-\frac{Y''}{Y}=\text{constant}.
$$

Choose the sign of the separation constant based on the boundary conditions:

- Homogeneous fixed endpoints usually lead to sine eigenfunctions.
- Infinite or semi-infinite directions usually require decaying exponentials.
- Periodic boundaries usually lead to sines/cosines or complex exponentials.

---

## M.7 Fourier series formulas

### Full Fourier series on $[-L,L]$

$$
f(x)=\frac{a_0}{2}+\sum_{n=1}^{\infty}\left[a_n\cos\left(\frac{n\pi x}{L}\right)+b_n\sin\left(\frac{n\pi x}{L}\right)\right].
$$

Coefficients:
$$
a_n=\frac1L\int_{-L}^{L}f(x)\cos\left(\frac{n\pi x}{L}\right)dx,
$$
$$
b_n=\frac1L\int_{-L}^{L}f(x)\sin\left(\frac{n\pi x}{L}\right)dx.
$$

### Fourier sine series on $[0,L]$

Use for fixed-zero boundary conditions:
$$
f(x)=\sum_{n=1}^{\infty}b_n\sin\left(\frac{n\pi x}{L}\right),
$$
$$
b_n=\frac2L\int_0^L f(x)\sin\left(\frac{n\pi x}{L}\right)dx.
$$

### Fourier cosine series on $[0,L]$

Use for zero-slope/Neumann-type boundary conditions:
$$
f(x)=\frac{a_0}{2}+\sum_{n=1}^{\infty}a_n\cos\left(\frac{n\pi x}{L}\right),
$$
$$
a_n=\frac2L\int_0^L f(x)\cos\left(\frac{n\pi x}{L}\right)dx.
$$

---

## M.8 Common separated solutions

### Laplace equation on a rectangle with zero side boundaries

If
$$
0<x<L,\quad 0<y<H,
$$
and
$$u(0,y)=u(L,y)=0,
$$
then use
$$
X_n(x)=\sin\left(\frac{n\pi x}{L}\right).
$$

The $y$-part is usually
$$
Y_n(y)=A_ne^{n\pi y/L}+B_ne^{-n\pi y/L}
$$
or equivalently hyperbolic functions:
$$
Y_n(y)=C_n\sinh\left(\frac{n\pi(H-y)}{L}\right).
$$

### Heat equation on $0<x<L$ with fixed zero ends

$$u_t=D u_{xx},\qquad u(0,t)=u(L,t)=0.
$$

Solution:
$$u(x,t)=\sum_{n=1}^{\infty}b_n\sin\left(\frac{n\pi x}{L}\right)\exp\left[-D\left(\frac{n\pi}{L}\right)^2t\right].
$$

Coefficients from initial condition $u(x,0)=f(x)$:
$$
b_n=\frac2L\int_0^L f(x)\sin\left(\frac{n\pi x}{L}\right)dx.
$$

### Wave equation on $0<x<L$ with fixed ends

$$u_{tt}=c^2u_{xx},\qquad u(0,t)=u(L,t)=0.
$$

General separated solution:
$$u(x,t)=\sum_{n=1}^{\infty}\sin\left(\frac{n\pi x}{L}\right)
\left[A_n\cos\left(\frac{n\pi ct}{L}\right)+B_n\sin\left(\frac{n\pi ct}{L}\right)\right].
$$

If
$$u(x,0)=f(x),\qquad u_t(x,0)=g(x),$$
then
$$
A_n=\frac2L\int_0^L f(x)\sin\left(\frac{n\pi x}{L}\right)dx,
$$
$$
B_n=\frac{2}{n\pi c}\int_0^L g(x)\sin\left(\frac{n\pi x}{L}\right)dx.
$$

---

## M.9 D'Alembert transformation

For
$$u_{tt}=c^2u_{xx},$$
set
$$
p=x+ct,
$$
$$
q=x-ct.
$$

Then
$$
\frac{\partial}{\partial x}=\frac{\partial}{\partial p}+\frac{\partial}{\partial q},
$$
$$
\frac{\partial}{\partial t}=c\left(\frac{\partial}{\partial p}-\frac{\partial}{\partial q}\right).
$$

The wave equation becomes
$$u_{pq}=0.
$$

Therefore
$$u(p,q)=F(p)+G(q),$$
so
$$
\boxed{u(x,t)=F(x+ct)+G(x-ct).}
$$

---

## M.10 Schrödinger infinite square well

Time-independent Schrödinger equation inside the well:
$$
-\frac{\hbar^2}{2m}\psi''=E\psi,
\qquad 0<x<L.
$$

Boundary conditions:
$$
\psi(0)=0,
\qquad
\psi(L)=0.
$$

Eigenfunctions:
$$
\psi_n(x)=\sqrt{\frac2L}\sin\left(\frac{n\pi x}{L}\right),
\qquad n=1,2,3,\ldots
$$

Energies:
$$
E_n=\frac{n^2\pi^2\hbar^2}{2mL^2}.
$$

General state:
$$
\Psi(x,t)=\sum_{n=1}^{\infty}c_n\psi_n(x)e^{-iE_nt/\hbar}.
$$

---

## M.11 Dirac delta function

Key properties:

$$
\delta(x-a)=0\quad\text{for }x\neq a,
$$
$$
\int_{-\infty}^{\infty}\delta(x-a)dx=1,
$$
$$
\int_{-\infty}^{\infty}f(x)\delta(x-a)dx=f(a).
$$

Scaling:
$$
\delta(ax)=\frac1{|a|}\delta(x).
$$

Derivative identity:
$$
\int f(x)\delta'(x-a)dx=-f'(a).
$$

3D delta:
$$
\delta(\mathbf r-\mathbf r')=\delta(x-x')\delta(y-y')\delta(z-z').
$$

---

## M.12 Fourier transform formulas

With the symmetric convention:
$$
U(k)=\frac1{\sqrt{2\pi}}\int_{-\infty}^{\infty}u(x)e^{-ikx}dx,
$$
$$u(x)=\frac1{\sqrt{2\pi}}\int_{-\infty}^{\infty}U(k)e^{ikx}dk.
$$

Derivative rules:
$$
\mathcal F[u_x]=ikU,
$$
$$
\mathcal F[u_{xx}]=-k^2U.
$$

Multiplication/convolution rule:
$$
\mathcal F[V(x)u(x)]=\frac1{\sqrt{2\pi}}(\widehat V*U)(k).
$$

In 3D:
$$
\nabla\to i\mathbf k,
$$
$$
\nabla^2\to -|\mathbf k|^2,
$$
$$
\nabla\cdot\mathbf u\to i\mathbf k\cdot\mathbf U,
$$
$$
\nabla\times\mathbf u\to i\mathbf k\times\mathbf U.
$$

---

## M.13 Fourier sine and cosine transforms on $[0,\infty)$

Sine transform:
$$
\mathcal S[f](\omega)=\sqrt{\frac2\pi}\int_0^\infty f(x)\sin(\omega x)dx.
$$

Inverse sine transform:
$$
f(x)=\sqrt{\frac2\pi}\int_0^\infty \mathcal S[f](\omega)\sin(\omega x)d\omega.
$$

Cosine transform:
$$
\mathcal C[f](\omega)=\sqrt{\frac2\pi}\int_0^\infty f(x)\cos(\omega x)dx.
$$

Inverse cosine transform:
$$
f(x)=\sqrt{\frac2\pi}\int_0^\infty \mathcal C[f](\omega)\cos(\omega x)d\omega.
$$

Useful derivative identities:
$$
\mathcal S[f']=-\omega\mathcal C[f],
$$
$$
\mathcal C[f']=-\sqrt{\frac2\pi}f(0)+\omega\mathcal S[f],
$$
$$
\mathcal S[f'']=\sqrt{\frac2\pi}\omega f(0)-\omega^2\mathcal S[f],
$$
$$
\mathcal C[f'']=-\sqrt{\frac2\pi}f'(0)-\omega^2\mathcal C[f].
$$

---

## M.14 Green's functions

For a linear PDE
$$
\mathcal L u=f,
$$
the Green's function satisfies
$$
\mathcal L_{\mathbf r}G(\mathbf r,\mathbf r')=\delta(\mathbf r-\mathbf r').
$$

Then a particular solution is
$$u(\mathbf r)=\int G(\mathbf r,\mathbf r')f(\mathbf r')d\mathbf r'.
$$

### 3D Laplacian Green's function

With
$$
\nabla^2G=\delta,
$$
we have
$$
G(\mathbf r,\mathbf r')=-\frac1{4\pi|\mathbf r-\mathbf r'|}.
$$

### 3D Helmholtz Green's function

With
$$
(\nabla^2+k^2)G=\delta,
$$
we have
$$
G(\mathbf r,\mathbf r')=-\frac{e^{\pm ik|\mathbf r-\mathbf r'|}}{4\pi|\mathbf r-\mathbf r'|}.
$$

If instead the convention is
$$
(\nabla^2+k^2)G=-\delta,
$$
then the sign is positive.

---

## M.15 Electrostatics formulas

Poisson equation:
$$
\nabla^2V=-\frac{\rho_e}{\varepsilon_0}.
$$

Potential from a continuous charge distribution:
$$
V(\mathbf r)=\frac1{4\pi\varepsilon_0}\int\frac{\rho_e(\mathbf r')}{|\mathbf r-\mathbf r'|}d\mathbf r'.
$$

For a thin uniformly charged rod of length $L$ and total charge $Q$ along the $z$-axis:
$$
\lambda=\frac QL,
$$
$$
V(s,z)=\frac{Q}{4\pi\varepsilon_0L}\ln\left[\frac{(z+L/2)+\sqrt{s^2+(z+L/2)^2}}{(z-L/2)+\sqrt{s^2+(z-L/2)^2}}\right],
$$
where $s=\sqrt{x^2+y^2}$.

---

## M.16 Poisson integral formula for the upper half-plane

For Laplace's equation in the upper half-plane,
$$u_{xx}+u_{zz}=0,
\qquad z>0,
$$
with boundary value
$$u(x,0)=c(x),$$
the solution is
$$
\boxed{u(x,z)=\frac1\pi\int_{-\infty}^{\infty}\frac{z\,c(s)}{z^2+(s-x)^2}ds.}
$$

For top-hat data
$$
c(s)=\begin{cases}c_0, & -a\le s\le a,\\0, & \text{otherwise},\end{cases}
$$
then
$$
\boxed{u(x,z)=\frac{c_0}{\pi}\left[\arctan\left(\frac{a-x}{z}\right)+\arctan\left(\frac{a+x}{z}\right)\right].}
$$

---

## M.17 Exam strategy checklist

When facing a PDE problem, ask these questions in order:

1. **What type of PDE is it?** Laplace, heat, wave, Schrödinger, Poisson, or something else?
2. **What variables are present?** Space only, or space and time?
3. **What is the domain?** Finite interval, rectangle, half-line, full line, cylinder, sphere?
4. **What are the boundary conditions?** Dirichlet, Neumann, Robin, mixed?
5. **Is the problem homogeneous?** If not, can you split into steady-state plus transient, or use Green's functions?
6. **Which basis fits the boundary conditions?** Sine, cosine, exponential, Bessel, Legendre, Fourier transform?
7. **Do you need Fourier coefficients?** Write the coefficient formula before integrating.
8. **Do a sanity check.** Verify boundaries, initial conditions, decay, units, and limiting cases.

---

## M.18 Common mistakes to avoid

1. Forgetting that $\ln(x^2+y^2)$ is singular at the origin.
2. Calling a nonlinear PDE \"homogeneous\" too casually.
3. Using sine series when the boundary condition is Neumann; cosine series may be needed.
4. Forgetting the exponential decay factor in heat equation solutions.
5. Confusing wave equation signs: $u_{tt}=c^2u_{xx}$ is hyperbolic; $u_{xx}+c^{-2}u_{tt}=0$ is elliptic in $(x,t)$.
6. Forgetting the absolute value $|k|$ when solving transformed half-plane problems.
7. Losing a minus sign in Green's functions because different books use different delta-source conventions.
8. Treating Fourier transform frequency signs as physical energy signs in Schrödinger problems.
9. Not checking whether a Fourier series satisfies boundary values at corners; Fourier series often gives endpoint averages at discontinuities.
10. Forgetting that a point force or point charge usually introduces a delta function.
