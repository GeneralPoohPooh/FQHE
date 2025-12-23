# ==========================================
# 1. INITIALIZATION & SYSTEM CONFIGURATION
# ==========================================
N_phi = 12                     # Number of orbitals in Lowest Landau Level (LLL)
N_sectors = [3, 4, 5]          # Particle sectors for Grand Canonical Ensemble
target_nu = 4 / 12             # N=4 at N_phi=12 yields nu = 1/3

V1 = 1.5                       # Haldane Pseudopotential (Nearest Neighbor penalty)
alpha = 0.025                  # Edge Potential (Confinement)
V_scatter = 0.3                # Off-diagonal scattering/hopping strength
mu = 1.0                       # Chemical Potential

# ==========================================
# 2. BASIS & HAMILTONIAN CONSTRUCTION
# ==========================================
  1. GENERATE BASIS:
       Create all many-body configurations (Slater Determinants) for N particles in N_phi orbitals.

  2. CALCULATE DIAGONAL (Static Energy):
       FOR each configuration:
           - ADD Haldane Penalty (V1): Penalize states with particles in adjacent orbitals.
           - ADD Harmonic Trap (alpha): Penalize states that spread away from the center.
           - Assign result to H[i, i].

  3. CALCULATE OFF-DIAGONAL (Scattering):
       FOR every pair of configurations (i, j):
           - IDENTIFY if the two states differ by exactly TWO particles.
           - CHECK Rotation Invariance: Ensure total Angular Momentum is conserved (m1 + m2 = m3 + m4).
           - IF conserved: Assign Scattering Strength (V_scatter) to H[i, j].

  4. SOLVE SPECTRUM:
       - Diagonalize the matrix H.
       - Store Eigenvalues (Energies) and associate them with particle number N.

RETURN All Energies and Particle Labels
# ==========================================
# 3. SPECTRAL ANALYSIS
# ==========================================
    
  1. Calculate Grand Canonical Weights: exp(-beta * (E - mu*N))
  2. Z = calculate_partition_function(log_weights)
  3.mean_E = compute_average(energies, log_weights)
  4.mean_N = compute_average(N_labels, log_weights)
  5.return entropy = kB * (log(Z) + beta * (mean_E - mu * mean_N))

# ==========================================
# 4. PLOTTING
# ==========================================
# 1. Plot Energy Spectrum for N=4: 
#    Look for the "Laughlin Gap" (separation between ground state and excited states).
# 2. Plot Entropy vs T: 
#    Verify S -> 0 as T -> 0, proving an incompressible, unique ground state.
