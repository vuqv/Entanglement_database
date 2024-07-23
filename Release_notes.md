# Release Notes:

## v1.0:
    1. This release includes only high quality structure (average plddt >=70)
    2. For structure that has entanglement, we check the quality of entanglements. An entanglement is valid if their 
    contact closes the loop has per-residues in confidence region (plddt >= 70) and after processing crossing residues, at least 1 crossing residue remained.
    If any of these conditions does not meet, the entanglement will be removed for that contact.
    3. 3 dataset depended on how we handle for slipknots (see Readme)
    
## v0.1:
    This release includes:
        1. whGLN parameters
