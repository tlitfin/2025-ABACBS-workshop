---
title: "EXTRA: Extension exercises"
teaching: 
exercises: 
questions:
objectives:
keypoints:
---

## Extension 1: Structure prediction with Boltz

## Extension 2: Function annotation with SPfast 
[SPfast](https://colab.research.google.com/github/tlitfin/SPfast/blob/main/notebooks/SPfast_AFDB_clusters_PFAM.ipynb) is an alternative strategy for structure-based search and provides a minimal set of hits based on non-redundant PFAM clan annotations.

1. Upload our predicted PDB structure by **leaving the input fields blank.** 
2. Select **Run all** to execute search for annotated structures using SPfast.
3. **Wait ~3 minutes** for the file upload prompt to appear under the 3rd cell and upload your predicted structure (`sample0_alphafold2.pdb`).
4. SPfast will take about ~7 minutes after uploading the query structure.

> ## Input form
> {% raw %}
> <p align="center">
> <img src="../assets/img/abacbs-spfast1.png" alt="spfast1" width="800"/>
> </p>
> {% endraw %}
{: .keypoints}

> ## Results
> {% raw %}
> | Query                      | Template   | Score | PFAM coverage | InterPro  | PFAM    | Clan            | Count |
> |-----------------------------|------------|-------|----------------|-----------|---------|-----------------|-------|
> | sample0_alphafold2          | A0A7V7WJC0 | 0.972 | 0.851          | IPR023087 | PF01706 | FliG            | 3     |
> | sample0_alphafold2          | A0A5E4W8M8 | 0.903 | 0.941          | IPR009510 | PF06578 | YscK            | 3     |
> | sample0_alphafold2          | A0A2Y0G0F7 | 0.766 | 0.969          | IPR013388 | PF09482 | OrgA_MxiK       | 3     |
> | sample0_alphafold2          | A0A2S7ERH1 | 0.746 | 0.895          | IPR013393 | PF09502 | HrpB4           | 1     |
> | sample0_alphafold2          | Q8ZPP3     | 0.697 | 0.862          | IPR025292 | PF13327 | T3SS_LEE_assoc  | 1     |
> {% endraw %}
> 
> This collection of similar structures are annotated with PFAM clans (FliG, YscK, OrgA_MxiK, HrpB4, T3SS_LEE_assoc) which all relate to a Type III secretion system (T3SS) adaptor protein (SctK gene).
> 
> This suggests a potential related function for our uncharacterized gene.
{: .solution}


## Extension 3: Disk footprint
- A downside of nextflow is that many small files are generated during workflow execution.
## Afterscript

```
withName: 'RUN_ALPHAFOLD2_MSA' {
    cpus   = { 8                      }
    memory = { 16.GB                  }
    time   = { 12.h                   }
    afterScript = """
        rm pdb_seqres/pdb_seqres.txt
        find . -type f -name '*.sto' -exec zstd -19 --rm {} \\;
    """
}
```

```
withName: 'RUN_ALPHAFOLD2_PRED' {
    afterScript = """
        find . -type f -name '*.pkl' -exec zstd -19 --rm {} \\;
    """
}
```
