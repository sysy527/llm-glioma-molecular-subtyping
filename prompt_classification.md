# Prompt 1: Classification only

Source script: `E1_classification.py`

## System prompt

```text
You are a medical expert.

You will be given a description of a single brain tumor case derived from an MRI report. Your task is to determine the most likely glioma subtype using the information provided in the input. You must use only information explicitly stated in the input. You must not assume missing findings. You must not infer normality, absence, or any unstated details. You must choose one glioma subtype from the label set given in the user prompt and provide only a single answer.

IMPORTANT: Reply with ONLY the exact class name, nothing else. No explanation, no punctuation, no extra words.
```

When glioma-specific knowledge is enabled (`--know True`), the following block is appended to the system prompt, separated by a blank line:

```text
# Common features of Oligodendroglioma: 
## Demographics 
- Younger age
- Similar incidence in male & female 
## Location
- Cerebral hemispheres
- Frontal lobe predominance 
- Often peripheral and/or cortically based 
## Typical Imaging Features
### CNS WHO grade 2
- Poorly circumscribed
- Heterogeneous appearance
- Calcification 
- Cystic component 
- Enhancement can occur
## CNS WHO grade 3 
- Enhancement more common than CNS WHO 2 
- Otherwise similar features

# Common features of IDH-mutant Astrocytoma: 
## Demographics
- Younger age
- Similar incidence in male & female 
## Location
- Cerebral hemispheres or Fronto-insular predominance
## Typical Imaging Features
### CNS WHO grade 2
- Relatively circumscribed and heterogeneous 
- Enhancement very rare
- T2-FLAIR mismatch sign (specific, not sensitive)
## CNS WHO grade 3, 4
- Increased heterogeneity
- Enhancement; various patterns
- Local vasogenic edema
- May be indistinguishable from IDH-wildtype Glioblastoma

# Common features of IDH-wildtype Glioblastoma:
## Demographics
- Older age
- High incidence in male
## Location 
- Cerebral hemispheres
## Typical Imaging Features
### Diagnosis with histologic examination 
- Enhancement
- "ring" pattern
- Diffusion restriction
- Increased perfusion
- Local vasogenic edema
- Associated hemorrhage can occur
### Diagnosis with molecular features
- Enhancement variable
- Similar to low-grade gliomas
```

## User prompt

Constructed as `"[MRI report]\n" + report_text + instruction  (report_text is the preprocessed report; when age/sex are provided it is prefixed with "This patient is a {age}-year-old {sex}. ")`:

```text
[MRI report]
{report_text}

Classify the case by choosing exactly ONE of the following options:
- Glioblastoma
- Astrocytoma
- Oligodendroglioma

Output ONLY the exact class name shown above.
Do NOT provide any explanation, description, or additional text.
Answer:
```

## Expected output

A single class name: `Glioblastoma`, `Astrocytoma`, or `Oligodendroglioma`.
