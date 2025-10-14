---
title: Tweede testomgeving
description: Leer de voordelen en het gebruik van een tweede testomgeving voor parallelle tests, uitgifteisolatie, versiebeheer en nog veel meer.
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 0%

---

# Tweede testomgeving

In de Adobe Commerce Cloud-infrastructuur zorgt de testomgeving voor uitgebreide tests en validatie in een omgeving die de productieomgeving weerspiegelt. Deze omgeving stelt u in staat om fouten veilig te identificeren en op te lossen, terwijl u ervoor zorgt dat alle nieuwe functies of wijzigingen naadloos worden geïntegreerd voordat deze van invloed zijn op uw livesite.

Sommige projecten vereisen een meer geavanceerd ontwikkelingswerkschema. Om deze behoefte te ondersteunen, biedt de Adobe een extra het opvoeren milieu als extra optie aan uw wolkeninfrastructuur. Het hebben van twee het opvoeren milieu&#39;s is voordelig voor complexe projecten en gelijktijdige samenwerking over teams.

Een secundaire testomgeving biedt de volgende voordelen:

- **Parallelle het Testen**: Met twee het opvoeren milieu&#39;s, kunnen de teams nieuwe eigenschappen en kritieke updates gelijktijdig testen zonder de ontwikkeling van elkaar in te storen. U kunt bijvoorbeeld een omgeving wijden aan het testen van functies, terwijl u de andere omgeving voorbehoudt voor prestatie- en stresstests.

- **Isolatie van Kwesties**: Wanneer de insecten of de kwesties zich in het primaire het opvoeren milieu voordoen, kunt u hen in het secundaire milieu herhalen en diagnostiseren zonder testende vooruitgang tegen te houden. Dit zorgt ervoor dat het oplossen van problemen zich niet in aan de gang zijnde tests mengt.

- **Controle van de Versie**: Beheer effectiever verschillende versies van uw toepassing. De primaire testomgeving kan de nieuwste stabiele build uitvoeren, terwijl de experimentele functies van de secundaire tests actief zijn. Hierdoor kunt u de releasecycli beter beheren en zorgt u ervoor dat de stabiele builds niet worden verstoord door experimentele wijzigingen.

- **Verbeterde Planning van de Output**: U kunt verschillende plaatsingsscenario&#39;s simuleren. Het primaire het opvoeren milieu kan de huidige productiesopstelling simuleren, terwijl het secundaire milieu kan worden gevormd om volgende versies te testen.

- **het Testen van de Erkenning van de Gebruiker (UAT)**: Terwijl het gebruiken van het primaire milieu voor aan de gang zijnde ontwikkeling, kunt u secundair milieu aan UAT wijden. Dit staat gebruikers of cliënten toe om terugkoppelen op nieuwe eigenschappen in een gecontroleerd plaatsen te testen en te verstrekken, zonder het testen te beïnvloeden.

- **het Testen van de Regressie**: U kunt één milieu voor voorwaarts-gerichte tests en andere voor het testen van regressie gebruiken, die ervoor zorgen dat de nieuwe veranderingen bestaande functionaliteit niet breken.

- **Opleiding en Demonstraties**: Gebruik één milieu voor opleiding nieuwe teamleden of het aantonen van nieuwe eigenschappen aan stakeholders. Dit zorgt ervoor dat trainingsactiviteiten het testen niet onderbreken.

- **Privé Opstelling van de Verbinding**: De meester en milieu&#39;s van de Integratie steunen geen Privé opstelling van de Verbinding. Als uw ontwikkelingswerkschema extra milieu&#39;s vereist die via Privé Verbinding voor ontwikkeling, het testen, of een ander doel worden verbonden, denk na toevoegend een extra het opvoeren milieu.

Als u twee testomgevingen hebt, kan dit de efficiëntie van uw workflow, het risicobeheer en de algehele kwaliteit van uw toepassing aanzienlijk verbeteren. Deze omgevingen bieden veiligheid en flexibiliteit die één testomgeving niet kan bieden.

>[!NOTE]
>
>Deze instelling is een invoegtoepassing. Klanten die een secundaire omgeving willen, moeten contact opnemen met hun verkoopvertegenwoordiger om er een aan te vragen. De verkoper kan informatie verstrekken over prijzen en het leveringsproces.

Als uw project reeds een extra het opvoeren milieu heeft of u overweegt uw huidig project te bevorderen, overweeg de volgende leveringschronologie en verantwoordelijkheden:

- Het inrichtingsproces kan tot twee weken duren nadat u het verzoek met uw Adobe verkoper hebt bevestigd.

- Nieuwe testomgevingen zijn alleen beschikbaar in hetzelfde gebied als uw huidige testomgeving en productieomgeving.

- U moet of uw Integratie of Hoofdomgeving bijwerken en specificeren op welke van uw milieu&#39;s uw secundaire het opvoeren milieu zal worden gebaseerd. De secundaire het opvoeren omgeving kan niet uit de het opvoeren of milieu&#39;s van de Productie worden gekopieerd.

- Nadat u uw nieuwe het opvoeren milieu ontvangt, kunt u het in uw ontwikkelingsstroom omvatten. Net als bij andere omgevingen zijn code- en database-updates uw verantwoordelijkheid.

## De omgeving aanvragen

Voer de volgende stappen uit om uw verzoek te vergemakkelijken:

1. Upgrade uw vertakking.

   Voer een upgrade uit op uw integratie- of hoofdvertakking met de code en database die u voor de nieuwe omgeving wilt gebruiken.

1. Neem contact op met uw verkoper.

   Neem contact op met de verkoper van de Adobe en geef deze de specifieke vertakking die u als basis voor uw nieuwe testomgeving (Integratie of Master) wilt gebruiken.

1. Bevestig details.

   Nadat u de gegevens bij uw vertegenwoordiger hebt bevestigd, wacht u op de bevestiging dat het inrichtingsverzoek is ontvangen en wordt verwerkt. Wanneer het inrichtingsproces is voltooid, stuurt het Adobe-team u een bevestiging.

1. Implementeer in uw nieuwe omgeving.

   Volg de [&#x200B; standaardplaatsingsstappen &#x200B;](../deploy/staging-production.md) om uw code en gegevensbestand aan het nieuwe het opvoeren milieu op te stellen.
