---
layout: post
title: "Human Activity Recognition"
date: 2015-01-17
categories: big data
---

Em novembro de 2014 eu participei do [Interopmix](http://www.interopmix.com.br/) com uma palestra sobre *Human Activity Recognition*. 
O material gerado para esta palestra é resultado de alguns estudos que eu realizei com datasets sobre o tema. Os slides podem ser vistos
abaixo.

<center>
<iframe src="//www.slideshare.net/slideshow/embed_code/42190453" width="425" height="355" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe>
</center>

Basicamente, os datasets 
existentes coletam dados dos sensores (por exemplo, acelerômetros) de dispositivos móveis e rotulam estes dados com as atividades que os usuários dos 
dispositivos móveis estão realizando.

Estes datasets são utilizados para responder a seguinte pergunta: *"Será que é possível construir modelos para predizer que atividade a pessoa
está realizando a partir de informações geradas apenas pelos sensores do dispositivo móvel daquela pessoa?"*

<code>
	activity ~ x1 + y1 + z1 + x2 + y2 + z2 + x3 + y3 + z3 + x4 + y4 + z4
</code>

Os artigos [[1](https://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones)] e [[2](https://archive.ics.uci.edu/ml/datasets/Wearable+Computing%3A+Classification+of+Body+Postures+and+Movements+%28PUC-Rio%29)] e os experimentos que eu realizei exemplificam que é possível identificar a atividade que uma pessoa está
realizando somente a partir de infomações geradas pelos sensores dos dispositivos móveis. Os resultados apresentados pelos artigos e pelos
meus experimentos são muito próximos. Em [[2](https://archive.ics.uci.edu/ml/datasets/Wearable+Computing%3A+Classification+of+Body+Postures+and+Movements+%28PUC-Rio%29)], os autores utilizam **AdaBoost com C4.5** e obtêm um acurácia de **99.4%**. Enquanto que eu utilizei, 
para o mesmo dataset, o algoritmo **RandomForest** e obtive a mesma acurácia de **99.4%**. Em [[1](https://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones)], com um dataset diferente e mais complexo, os autores
conseguem uma acurácia de **89.3%** utilizando o algoritmo **SVM**. Neste mesmo dataset, com o algoritmo **RandomForest**, foi possível obter uma acurácia de
**90.9%**. 

Em ambos os datasets, a classe que se deseja aprender é a atividade que o usuário está realizando (por exemplo, andando, sentado, em pé, deitado, etc). Depois de realizado os experimentos é fácil perceber que é possível construir classificadores que conseguem classificar corretamente 90% das situações. 

Este tipo de capacidade tem permitido o desenvolvimento de novos produtos, tais como: o [Google Fit](https://fit.google.com/) e 
[aplicações para detecção de abalos sísmicos](http://cacm.acm.org/magazines/2014/7/176219-community-sense-and-response-systems/fulltext) 
utilizando um conjunto de celulares pessoais.  Sobre este último exemplo, existe um [vídeo](http://vimeo.com/98781340) muito interessante 
que descreve o projeto.

Mudando um pouco a pergunta
---------------------------

Ambos os datasets, além de possuirem informações sobre as atividades que os usuários estão realizando, sobre dados gerados a partir de acelerômetros e outros
sensores, também possuem um identificador do usuário - não se trata de um nome, cpf ou algo assim, apenas um número para identificar de forma única um 
determinado usuário.

Desta forma, é possível também criar modelos que respondem a seguinte pergunta: *"Qual é o usuário que está utilizando este dispositivo levando-se em consideração os dados dos sensores?"

Nenhum dos artigos apresentados acima tem como objetivo responder esta pergunta. No entanto, é simples alterar as variáveis dependentes e independentes de:

<code>
	activity ~ x1 + y1 + z1 + x2 + y2 + z2 + x3 + y3 + z3 + x4 + y4 + z4
</code> 

para:

<code>
	user ~ x1 + y1 + z1 + x2 + y2 + z2 + x3 + y3 + z3 + x4 + y4 + z4
</code> 

O experimento que testa esta pergunta está disponível [aqui](http://fbarth.net.br/humanActivityRecognition/scripts/har_case01_user.html). Neste experimento, utilizando **RandomForest**, foi possível criar um modelo com **acurácia igual a 99.3%**. Em uma competição disponível no [Kaggle](https://www.kaggle.com/), onde o objetivo era criar [modelos capazes de reconhecer usuários de dispositivos móveis levando-se em consideração apenas dados de sensores](https://www.kaggle.com/c/accelerometer-biometric-competition), a acurácia dos melhores modelos é em média **99.9%**!

Mais serviços e menos privacidade
---------------------------------

Na minha opinião, todos os dados descritos anteriormente são impressionantes! Na verdade, o que tudo isto quer dizer é que é muito fácil saber **quem** está utilizando um celular e o **que** esta pessoa está fazendo somente a partir dos dados coletados pelos **sensores do celular**. Isto permite o desenvolvimento e o aprimoramento de muitas aplicações realmente interessantes, tais como: Google Fit e aquele sistema que identifica abalos sísmicos. No entanto, também traz sérios problemas de privacidade. 

Qualquer aplicativo mobile pode requerer o acesso aos dados do acelerômetro e GPS do aparelho de uma pessoa e esta pessoa nem se quer questionar esta necessidade e simplesmente instalar um aplicativo que pode não ser muito confiável. Ou melhor, pode utilizar os dados das pessoas de forma inaqueda - desrespeitando a privacidade destas pessoas.

No entanto, o que é desrespeitar a privacidade das pessoas? Uma empresa, ou aplicativo, ter acesso a localização geográfica e as atividades de uma pessoa poderia ser considerada quebra de privacidade? Se sim então o Google está fazendo isto! Com o consentimento de muitas pessoas! Porque elas querem e porque elas vêem valor no serviço entregue pelo Google Fit.

Não vejo muitas pessoas reclamando sobre a falta de privacidade que dispositivos móveis ou aplicações sociais tem causado. Portanto, o que eu tenho a concluir é que **o conceito de privacidade entre nós mudou**. As pessoas não se importam mais em dizer a todo momento onde estão e o que estão fazendo - elas fazem isto pelo Facebook a todo momento e de forma manual. Deixar que um aplicativo (ou empresa) verifique a sua posição geográfica e a sua atividade a qualquer momento também não parece algo muito ruim. Talvez a próxima etapa seja permitir que aplicativos publiquem automáticamente a sua localização e o que você está fazendo...





