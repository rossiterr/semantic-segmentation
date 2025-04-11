# Segmentação de Imagens Urbanas com Redes Neurais Convolucionais

Este projeto apresenta um estudo comparativo entre diferentes modelos de redes neurais convolucionais aplicados à tarefa de **segmentação semântica** de imagens urbanas. Utilizando o dataset **Cityscapes**, foram avaliados os modelos **DeepLabV3 + ResNet-101**, **DeepLabV3 + MobileNetV3-Large** e **U-Net**.

---

## Autores

- Hugo Cardoso - [hac@cin.ufpe.br](mailto:hac@cin.ufpe.br)  
- Julio Sobral Filho - [jcasf@cin.ufpe.br](mailto:jcasf@cin.ufpe.br)  
- Rodrigo Guimarães Filho - [rrgf@cin.ufpe.br](mailto:rrgf@cin.ufpe.br)  

---

## Objetivo

Avaliar o desempenho de diferentes arquiteturas de CNNs na tarefa de **segmentação semântica urbana**, identificando pontos fortes e fracos de cada modelo, além de considerar fatores como precisão, eficiência e tempo de treinamento.

---

## Dataset

Utilizou-se o [Cityscapes Dataset](https://www.cityscapes-dataset.com/), que contém imagens anotadas de cenas urbanas reais com resolução de **256x512**, classificadas em **19 classes** (ruas, pessoas, prédios, árvores, etc.).

- **Total de imagens**: 3475  
- **Divisão dos dados**:
  - Treinamento: 2975 imagens (~85%)
  - Validação: 500 imagens (~15%)

As imagens foram pré-processadas de forma a separar automaticamente a **máscara original** e a **imagem real** contidas em uma única imagem do dataset.

---

## Modelos Avaliados

### 1. DeepLabV3 + ResNet101
- Arquitetura com **convoluções dilatadas**.
- Utiliza **ASPP (Atrous Spatial Pyramid Pooling)** para capturar múltiplas escalas.
- Mais preciso, mas computacionalmente mais pesado.

### 2. DeepLabV3 + MobileNetV3-Large
- Mais leve e otimizado para dispositivos móveis.
- Boa acurácia com menor custo computacional.

### 3. U-Net
- Arquitetura encoder-decoder com **skip connections**.
- Excelente para bases pequenas e segmentações precisas em bordas.

---

## Métricas de Avaliação

- **Training Loss (MSE)**  
- **Validation Loss (MSE)**  
- **Pixel Accuracy**  
- *Observação:* Métricas como IoU e mIoU não foram utilizadas por limitações na informação de classes das máscaras.

---

## Treinamento

- **Épocas**: 25  
- **Otimizador**: Adam  
- **Learning Rate**: 0.01  
- **Função de Custo**: Mean Square Error (MSE)  
- **Visualização**: Após cada época, são exibidas a máscara verdadeira e a máscara gerada.

---

## Resultados

### Tabela Comparativa

| Modelo                        | Pixel Accuracy | Val Loss (↓) | Observações                              |
|------------------------------|----------------|--------------|------------------------------------------|
| DeepLabV3 + ResNet101        | 0.85           | 0.012        | Melhor resultado geral                   |
| DeepLabV3 + MobileNetV3-Large| 0.81           | 0.017        | Melhor custo-benefício                   |
| U-Net                        | 0.78           | 0.019        | Mais simples, resultados consistentes    |

---

## Como Executar

### Pré-requisitos

- Python 3.x  
- PyTorch  
- torchvision  
- matplotlib  
- numpy

### Execução

```bash
# Treinamento
python train.py --model deeplabv3_resnet101
python train.py --model deeplabv3_mobilenet_v3_large
python train.py --model unet

# Avaliação
python evaluate.py --model deeplabv3_resnet101

