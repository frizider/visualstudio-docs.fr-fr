---
title: "Dépannage de références de Service | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- msvse_wcf.Err.ReferenceGroup_NamespaceConflictsOther
- msvse_wcf.Err.AddSvcRefDlg_NothingSelectedOnGo
- msvse_wcf.Err.ErrorOnOK
- msvse_wcf.cfg.ConfigurationErrorsException
helpviewer_keywords:
- service references [Visual Studio], troubleshooting
- WCF services, troubleshooting
ms.assetid: 3b531120-1325-4734-90c6-6e6113bd12ac
caps.latest.revision: "22"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.technology: vs-data-tools
ms.openlocfilehash: e46c8bf778ff18ea25096e524716bcb44916f460
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="troubleshooting-service-references"></a>Dépannage des références de service
Cette rubrique répertorie les problèmes courants qui peuvent se produire lorsque vous travaillez avec [!INCLUDE[vsindigo](../data-tools/includes/vsindigo_md.md)] ou [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] références dans [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].  
  
## <a name="error-returning-data-from-a-service"></a>Erreur lors du renvoi des données à partir d’un Service  
 Lorsque vous retournez un `DataSet` ou `DataTable` à partir d’un service, vous pouvez recevoir une exception « le quota de taille maximale pour les messages entrants a été dépassé ». Par défaut, le `MaxReceivedMessageSize` propriété pour certaines liaisons est définie à une valeur relativement faible pour limiter l’exposition aux attaques par déni de service. Vous pouvez augmenter cette valeur pour éviter l’exception. Pour plus d'informations, consultez <xref:System.ServiceModel.HttpBindingBase.MaxReceivedMessageSize%2A>.  
  
 Pour corriger cette erreur :  
  
1.  Dans **l’Explorateur de solutions**, double-cliquez sur le fichier app.config pour l’ouvrir.  
  
2.  Recherchez le `MaxReceivedMessageSize` propriété et remplacez-le par une valeur supérieure.  
  
## <a name="cannot-find-a-service-in-my-solution"></a>Impossible de trouver un Service dans ma Solution  
 Lorsque vous cliquez sur le **Discover** situé dans le **ajouter des références de Service** boîte de dialogue, un ou plusieurs projets bibliothèque du Service WCF dans la solution n’apparaissent pas dans la liste des services. Cela peut se produire si une bibliothèque de Service a été ajoutée à la solution, mais n’a pas encore été compilée.  
  
 Pour corriger cette erreur :  
  
-   Dans **l’Explorateur de solutions**, cliquez sur le projet bibliothèque du Service WCF, cliquez sur **Build**.  
  
## <a name="error-accessing-a-service-over-a-remote-desktop"></a>Erreur d’accès à un Service sur un ordinateur de bureau à distance  
 Lorsqu’un utilisateur accède à un service WCF hébergé par Web via une connexion Bureau à distance et l’utilisateur ne dispose pas des autorisations d’administration, l’authentification NTLM est utilisée. Si l’utilisateur ne dispose pas des autorisations d’administration, l’utilisateur peut recevoir le message d’erreur suivant : « la requête HTTP n’est pas autorisée avec le schéma d’authentification client « Anonyme ». L’en-tête d’authentification reçu du serveur était 'NTLM'. »  
  
 Pour corriger cette erreur :  
  
1.  Dans le projet de site Web, ouvrez le **propriétés** pages.  
  
2.  Sur le **Options de démarrage** onglet, désactivez le **l’authentification NTLM** case à cocher.  
  
    > [!NOTE]
    >  Vous devez désactiver l’authentification NTLM uniquement pour les sites Web contenant exclusivement des services WCF. Sécurité pour les services WCF est gérée via la configuration dans le fichier web.config. Cela rend l’authentification NTLM inutiles.  
  
## <a name="access-level-for-generated-classes-setting-has-no-effect"></a>Niveau d’accès pour les Classes générées paramètre n’a aucun effet  
 Définition de la **accéder à niveau pour les classes générées** option dans le **configurer les références de Service** boîte de dialogue **interne** ou **Friend** peut ne pas toujours fonctionner. Même si l’option à définir dans la boîte de dialogue, les classes de prise en charge qui en résulte seront générées avec un niveau d’accès `Public`.  
  
 Il s’agit d’une limitation connue de certains types, tels que ceux qui sont sérialisés à l’aide de la <xref:System.Xml.Serialization.XmlSerializer>.  
  
## <a name="error-debugging-service-code"></a>Déboguer le Code Service erreur  
 Lorsque vous parcourez le code pour un service WCF à partir du code client, vous pouvez recevoir une erreur liée à des symboles manquants. Cela peut se produire lorsqu’un service qui faisait partie de votre solution a été déplacé ou supprimé de la solution.  
  
 Lorsque vous ajoutez une référence à un service WCF qui fait partie de la solution actuelle, une dépendance de génération explicite est ajoutée entre le projet de service et le projet de client de service. Cela garantit que le client accède toujours des fichiers binaires du service de mise à jour, qui est particulièrement important pour le débogage des scénarios tels que l’exécution pas à pas du code client dans le code de service.  
  
 Si le projet de service est supprimé de la solution, cette dépendance de génération explicite est invalidée. Visual Studio ne peut plus garantir que le projet de service recréé en fonction des besoins.  
  
 Pour corriger cette erreur, vous devez régénérer manuellement le projet de service :  
  
1.  Dans le menu **Outils** , cliquez sur **Options**.  
  
2.  Dans le **Options** boîte de dialogue, développez **projets et Solutions**, puis sélectionnez **général**.  
  
3.  Assurez-vous que le **configurations de build Show advanced** case à cocher est sélectionnée, puis cliquez sur **OK**.  
  
4.  Charger le projet de service WCF.  
  
5.  Dans le **Configuration Manager** boîte de dialogue, définissez la **configuration de solution Active** à **déboguer**. Pour plus d’informations, consultez [Guide pratique pour créer et modifier des configurations](../ide/how-to-create-and-edit-configurations.md).  
  
6.  Dans **l’Explorateur de solutions**, sélectionnez le projet de service WCF.  
  
7.  Sur le **générer** menu, cliquez sur **reconstruire** pour recréer le projet de service WCF.  
  
## <a name="wcf-data-services-do-not-display-in-the-browser"></a>Services de données WCF ne s’affichent pas dans le navigateur  
 Lorsqu’il tente d’afficher une représentation XML des données dans un [!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)], Internet Explorer peut mal interpréter les données comme un flux RSS. Vous devez vous assurer que l'option permettant d'afficher les flux RSS est désactivée.  
  
 Pour corriger cette erreur, désactivez les flux RSS :  
  
1.  Dans Internet Explorer, sur le **outils** menu, cliquez sur **Options Internet**.  
  
2.  Sur le **contenu** sous l’onglet du **flux** , cliquez sur **paramètres**.  
  
3.  Dans le **paramètres de flux** boîte de dialogue, désactivez le **activer le mode lecture du flux** case à cocher, puis cliquez sur **OK**.  
  
4.  Cliquez sur **OK** pour fermer la **Options Internet** boîte de dialogue.  
  
## <a name="see-also"></a>Voir aussi  
 [Services Windows Communication Foundation et services de données WCF dans Visual Studio](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)