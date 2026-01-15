---
library_name: transformers
license: other
license_name: dondza-non-commercial-model-license
license_link: https://huggingface.co/Raggio/dondza-xitsonga-asr-wav2vec2/blob/main/LICENSE
base_model: facebook/wav2vec2-xls-r-300m
tags:
- automatic-speech-recognition
- asr
- xitsonga
- mozambique
- wav2vec2
- xls-r
- generated_from_trainer
model-index:
- name: dondza-xitsonga-asr-wav2vec2
  results:
  - task:
      type: automatic-speech-recognition
      name: Automatic Speech Recognition
    dataset:
      name: NCHLT Speech Corpus (Xitsonga)
      type: speech
    metrics:
    - type: wer
      value: 0.07185358817165524
      name: WER
    - type: loss
      value: 0.07212410867214203
      name: Eval Loss
language:
- ts
metrics:
- wer
---

# dondza-xitsonga-asr-wav2vec2

**Dondza-Xitsonga Wav2Vec2** é um modelo de Reconhecimento Automático de Fala (ASR) em Xitsonga afinado no contexto do projecto **Dondza** (Raggio AI) a partir do checkpoint pré-treinado **facebook/wav2vec2-xls-r-300m**.

Tanto quanto sabemos, este é um dos primeiros modelos ASR end-to-end **desenvolvidos em Moçambique e publicamente disponibilizados** para Xitsonga.  
(Se tiver conhecimento de lançamentos moçambicanos anteriores, por favor partilhe — agradecemos correcções.)

---

## Licença (LER PRIMEIRO) — Licenciamento duplo para o checkpoint do modelo

Este repositório fornece um checkpoint ASR afinado e ficheiros relacionados.

### 1) Uso não comercial (predefinição, gratuito)
Os **pesos/checkpoint do modelo e ficheiros associados neste repositório** são disponibilizados sob a **Licença de Modelo Não Comercial Dondza**.

- ✅ Permitido: investigação, uso académico, projectos pessoais, demonstrações, experiências sem fins lucrativos
- ❌ Não permitido sem licença comercial: uso num produto pago, serviço pago, operações comerciais internas, aplicações monetizadas, APIs pagas, SaaS, implementações empresariais, ou qualquer outra exploração comercial
- Termos completos: consultar **LICENSE** neste repositório.

### 2) Uso comercial (pago)
Se pretender usar este modelo **comercialmente** (incluindo implementá-lo num produto/serviço comercial ou usá-lo para alimentar uma oferta paga), deve obter uma **Licença Comercial** da Raggio AI.

Como solicitar uma licença comercial:
- Abrir uma discussão neste repositório: https://huggingface.co/Raggio/dondza-xitsonga-asr-wav2vec2/discussions
- Ou abrir um issue no rastreador do projecto Dondza (se fornecido pela equipa)

Podemos oferecer:
- Licença comercial para auto-hospedagem dos pesos do modelo, e/ou
- Acesso por subscrição a uma API ASR alojada (termos comerciais/SLA disponíveis mediante solicitação)

---

## Licenças e atribuição de terceiros / upstream (importante)

Embora este repositório use uma licença personalizada para o checkpoint afinado, também depende de componentes upstream com as suas próprias licenças.

### Modelo base e bibliotecas
- **Checkpoint base:** `facebook/wav2vec2-xls-r-300m` (Apache-2.0)
- **Biblioteca Transformers:** Apache-2.0

Ao redistribuir ou usar este repositório, deve também cumprir quaisquer requisitos de aviso e atribuição upstream aplicáveis.

### Conjunto de dados de treino (não redistribuído aqui)
Este modelo foi afinado no **NCHLT Xitsonga Speech Corpus** (aproximadamente 56 horas de fala lida).

- **Não** redistribuímos o conjunto de dados neste repositório.
- Deve obter o conjunto de dados da sua fonte oficial.
- Licença do conjunto de dados: **CC BY 3.0** (atribuição necessária).

**Atribuição necessária (conjunto de dados):**  
O Departamento de Artes e Cultura do governo da República da África do Sul (DAC), o Conselho de Investigação Científica e Industrial (CSIR), e a Universidade do Noroeste (NWU), pelo NCHLT Speech Corpus.

---

## Modelo base

- Checkpoint base: **facebook/wav2vec2-xls-r-300m**
- Arquitectura: Wav2Vec2 + CTC
- Nota: a cabeça de saída CTC (`lm_head.weight`, `lm_head.bias`) é inicializada de novo para o vocabulário Xitsonga e aprendida durante o afinamento. Isto é esperado para afinamento CTC.

---

## Conjunto de dados

Este modelo foi afinado no **NCHLT Speech Corpus (Xitsonga)**:
- Página do conjunto de dados: https://repo.sadilar.org/items/5a6587ad-3067-49ff-bf2a-05ab171f4807
- Página do projecto: https://sites.google.com/site/nchltspeechcorpus/home/xitsonga

O corpus NCHLT é principalmente **fala lida**. Áudio conversacional do mundo real (ruído, alternância de código, gravações telefónicas) pode produzir taxas de erro mais elevadas.

---

## Divisões de dados (enunciados, falantes, duração)

| split   |   utterances |   unique_speakers |   duration_hours | duration_hms |
|:--------|-------------:|------------------:|-----------------:|:-------------|
| train   |        44924 |               190 |           52.658 | 52:39:29     |
| val     |         2247 |               188 |            2.595 | 02:35:42     |
| test    |         2905 |                 8 |            3.609 | 03:36:31     |

### Separação de falantes
Os conjuntos de falantes de treino e validação são **disjuntos** (sem sobreposição), pelo que os resultados de validação reflectem generalização para falantes não vistos.


---

## Resultados

Melhor checkpoint (seleccionado pelo menor WER de validação):
- **WER de validação:** **0.0719** (≈ **7.19%**)
- **Perda de validação:** 0.0721
- **Step:** 26,500
- **Época:** 29.7757
- **Tempo de execução de avaliação:** 27.787s
- **Throughput de avaliação:** 80.865 amostras/s

---

## Uso pretendido

- Entrada de voz para a aplicação Dondza (ASR Xitsonga)
- Investigação e prototipagem para tecnologia de fala Xitsonga
- Transcrição em lote de gravações de **fala lida ou limpa** em Xitsonga

---

## Limitações

- **Desajuste de domínio:** treinado em fala lida; áudio conversacional ou ruidoso pode degradar o desempenho.
- **Dialecto/região:** os dados NCHLT Xitsonga são principalmente da África do Sul; variedades moçambicanas (por exemplo, influências Changana/Ronga/Tswa) podem diferir na pronúncia e ortografia.
- **Não para uso de alto risco:** não validado para tarefas de transcrição críticas para segurança médica, legal ou outras.

---

## Como usar

```python
import torch
import librosa
from transformers import Wav2Vec2Processor, Wav2Vec2ForCTC

model_id = "Raggio/dondza-xitsonga-asr-wav2vec2"

processor = Wav2Vec2Processor.from_pretrained(model_id)
model = Wav2Vec2ForCTC.from_pretrained(model_id)

audio, sr = librosa.load("audio.wav", sr=16000)
inputs = processor(audio, sampling_rate=16000, return_tensors="pt", padding=True)

with torch.no_grad():
    logits = model(**inputs).logits

pred_ids = torch.argmax(logits, dim=-1)
text = processor.batch_decode(pred_ids)[0]
print(text)
