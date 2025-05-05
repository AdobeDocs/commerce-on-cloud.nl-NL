---
title: Omgevingsvariabelen
description: Zie een lijst met omgevingsvariabelen die specifiek zijn voor Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Build, Configuration, Deploy
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Omgevingsvariabelen

Met Adobe Commerce on cloud Infrastructure kunt u omgevingsvariabelen toewijzen om configuratieopties te overschrijven. Het `ece-tools` pakket plaatst waarden in het `env.php` dossier dat op waarden van [ variabelen van de Wolk ](variables-cloud.md) wordt gebaseerd, variabelen die in [!DNL Cloud Console] worden geplaatst, en het `.magento.env.yaml` configuratiedossier.

De omgevingsvariabelen in het `.magento.env.yaml` -bestand passen de Cloud-omgeving aan door de bestaande Commerce-configuratie te overschrijven. Als een standaardwaarde `Not Set` is, dan neemt het `ece-tools` pakket **&#x200B;**&#x200B;actie NO en gebruikt het [!DNL Commerce] gebrek of de waarde van de `MAGENTO_CLOUD_RELATIONSHIPS` configuratie. Als de standaardwaarde is ingesteld, wordt die standaardwaarde ingesteld door het `ece-tools` -pakket.

De typen omgevingsvariabelen zijn:

- [ ADMIN ](variables-admin.md) - variabelen treden projectADMIN variabelen met voeten
- [ MAGENTO_CLOUD ](variables-cloud.md) - variabelen specifiek voor wolkeninfrastructuur
- Variabelen gebruikt in het `.magento.env.yaml` -bestand:
   - [ Globaal ](variables-global.md) - de variabelen beïnvloeden bouw, opstellen, en post-stelt stadia op
   - [ bouwt ](variables-build.md)-variabelen controle bouwt acties
   - [ stelt ](variables-deploy.md) op:stellen-variabelen de controle acties op
   - [ post-opstellen ](variables-post-deploy.md) - variabelen controleacties na opstellen

De variabelen zijn _hiërarchisch_, zo betekent het dat als een variabele niet wordt met voeten getreden, het van het oudermilieu wordt geërft.

U kunt [ variabelen ADMIN ](variables-admin.md) van [!DNL Cloud Console] plaatsen of Adobe Commerce CLI gebruiken. U kunt andere omgevingsvariabelen van het [`.magento.env.yaml`](configure-env-yaml.md) dossier beheren om bouw-en-implementatieacties over al uw milieu-met inbegrip van Pro het Staging en Productie-zonder een steunkaartje te vereisen.

>[!TIP]
>
>YAML-bestanden zijn hoofdlettergevoelig en staan geen tabs toe. Wees voorzichtig met het gebruik van consistente inspringing in het `.magento.env.yaml` -bestand, anders werkt de configuratie mogelijk niet naar behoren. De voorbeelden in deze documentatie en in het steekproefdossier gebruiken _twee-ruimte_ inspringing. Gebruik de [ knoop-hulpmiddelen bevestigen bevel ](configure-env-yaml.md#validate-configuration-file) om uw configuratie te controleren.
