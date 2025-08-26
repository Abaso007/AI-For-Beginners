<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "ad568d55ae65c856fe929fc2b278510a",
  "translation_date": "2025-08-26T09:26:05+00:00",
  "source_file": "lessons/4-ComputerVision/11-ObjectDetection/lab/README.md",
  "language_code": "br"
}
-->
# Detecção de Cabeças usando o Hollywood Heads Dataset

Trabalho prático do [Currículo de IA para Iniciantes](https://github.com/microsoft/ai-for-beginners).

## Tarefa

Contar o número de pessoas em uma transmissão de câmera de vigilância é uma tarefa importante que nos permite estimar o número de visitantes em lojas, horários de pico em restaurantes, etc. Para resolver essa tarefa, precisamos ser capazes de detectar cabeças humanas de diferentes ângulos. Para treinar um modelo de detecção de objetos para identificar cabeças humanas, podemos usar o [Hollywood Heads Dataset](https://www.di.ens.fr/willow/research/headdetection/).

## O Conjunto de Dados

O [Hollywood Heads Dataset](https://www.di.ens.fr/willow/research/headdetection/release/HollywoodHeads.zip) contém 369.846 cabeças humanas anotadas em 224.740 quadros de filmes de Hollywood. Ele é fornecido no formato [https://host.robots.ox.ac.uk/pascal/VOC/](../../../../../../lessons/4-ComputerVision/11-ObjectDetection/lab/PASCAL VOC), onde para cada imagem há também um arquivo de descrição XML que se parece com isto:

```xml
<annotation>
	<folder>HollywoodHeads</folder>
	<filename>mov_021_149390.jpeg</filename>
	<source>
		<database>HollywoodHeads 2015 Database</database>
		<annotation>HollywoodHeads 2015</annotation>
		<image>WILLOW</image>
	</source>
	<size>
		<width>608</width>
		<height>320</height>
		<depth>3</depth>
	</size>
	<segmented>0</segmented>
	<object>
		<name>head</name>
		<bndbox>
			<xmin>201</xmin>
			<ymin>1</ymin>
			<xmax>480</xmax>
			<ymax>263</ymax>
		</bndbox>
		<difficult>0</difficult>
	</object>
	<object>
		<name>head</name>
		<bndbox>
			<xmin>3</xmin>
			<ymin>4</ymin>
			<xmax>241</xmax>
			<ymax>285</ymax>
		</bndbox>
		<difficult>0</difficult>
	</object>
</annotation>
```

Neste conjunto de dados, há apenas uma classe de objetos, `head`, e para cada cabeça, você obtém as coordenadas da caixa delimitadora. Você pode analisar os arquivos XML usando bibliotecas Python ou usar [esta biblioteca](https://pypi.org/project/pascal-voc/) para lidar diretamente com o formato PASCAL VOC.

## Treinamento de Detecção de Objetos

Você pode treinar um modelo de detecção de objetos usando uma das seguintes abordagens:

* Usando o [Azure Custom Vision](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/quickstarts/object-detection?tabs=visual-studio&WT.mc_id=academic-77998-cacaste) e sua API Python para treinar o modelo programaticamente na nuvem. O Custom Vision não será capaz de usar mais do que algumas centenas de imagens para treinar o modelo, então pode ser necessário limitar o conjunto de dados.
* Usando o exemplo do [tutorial do Keras](https://keras.io/examples/vision/retinanet/) para treinar o modelo RetunaNet.
* Usando o módulo integrado [torchvision.models.detection.RetinaNet](https://pytorch.org/vision/stable/_modules/torchvision/models/detection/retinanet.html) no torchvision.

## Conclusão

A detecção de objetos é uma tarefa frequentemente necessária na indústria. Embora existam alguns serviços que podem ser usados para realizar a detecção de objetos (como o [Azure Custom Vision](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/quickstarts/object-detection?tabs=visual-studio&WT.mc_id=academic-77998-cacaste)), é importante entender como a detecção de objetos funciona e ser capaz de treinar seus próprios modelos.

**Aviso Legal**:  
Este documento foi traduzido utilizando o serviço de tradução por IA [Co-op Translator](https://github.com/Azure/co-op-translator). Embora nos esforcemos para garantir a precisão, esteja ciente de que traduções automáticas podem conter erros ou imprecisões. O documento original em seu idioma nativo deve ser considerado a fonte oficial. Para informações críticas, recomenda-se a tradução profissional realizada por humanos. Não nos responsabilizamos por quaisquer mal-entendidos ou interpretações equivocadas decorrentes do uso desta tradução.