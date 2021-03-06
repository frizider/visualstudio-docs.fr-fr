---
title: "Procédure pas à pas : Mise en surbrillance de texte | Documents Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: editors [Visual Studio SDK], new - highlight text
ms.assetid: 64b772ad-4392-42e9-a237-5137f0384bf0
caps.latest.revision: "42"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 1f702a834b925f13525db122934a5593d313e0ac
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="walkthrough-highlighting-text"></a>Procédure pas à pas : Mise en surbrillance de texte
Vous pouvez ajouter différents effets visuels à l’éditeur en créant des composants de Managed Extensibility Framework (MEF). Cette procédure pas à pas montre comment mettre en surbrillance toutes les occurrences du mot actuel dans un fichier texte. Si un mot apparaît plusieurs fois dans un fichier texte, et que vous placez le point d’insertion dans une seule occurrence, toutes les occurrences sont mis en surbrillance.  
  
## <a name="prerequisites"></a>Conditions préalables  
 À partir de Visual Studio 2015, vous n’installez pas le Kit de développement logiciel Visual Studio à partir du centre de téléchargement. Il est inclus comme une fonctionnalité facultative dans le programme d’installation de Visual Studio. Vous pouvez également installer le kit SDK VS ultérieurement. Pour plus d’informations, consultez [l’installation de Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="creating-a-mef-project"></a>Création d’un projet MEF  
  
1.  Créez un projet VSIX c#. (Dans le **nouveau projet** boîte de dialogue, sélectionnez **Visual c# / extensibilité**, puis **projet VSIX**.) Nommez la solution `HighlightWordTest`.  
  
2.  Ajouter un modèle d’élément classifieur d’éditeur pour le projet. Pour plus d’informations, consultez [création d’une Extension avec un éditeur de modèle d’élément](../extensibility/creating-an-extension-with-an-editor-item-template.md).  
  
3.  Supprimez les fichiers de classe existants.  
  
## <a name="defining-a-textmarkertag"></a>Définition d’un TextMarkerTag  
 La première étape de mise en surbrillance de texte est à la sous-classe <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> et définir son apparence.  
  
#### <a name="to-define-a-textmarkertag-and-a-markerformatdefinition"></a>Pour définir un TextMarkerTag et une MarkerFormatDefinition  
  
1.  Ajoutez un fichier de classe et nommez-le **HighlightWordTag**.  
  
2.  Ajoutez les références suivantes :  
  
    1.  Microsoft.VisualStudio.CoreUtility  
  
    2.  Microsoft.VisualStudio.Text.Data  
  
    3.  Microsoft.VisualStudio.Text.Logic  
  
    4.  Microsoft.VisualStudio.Text.UI  
  
    5.  Microsoft.VisualStudio.Text.UI.Wpf  
  
    6.  System.ComponentModel.Composition  
  
    7.  Presentation.Core  
  
    8.  Presentation.Framework  
  
3.  Importez les espaces de noms suivants.  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.ComponentModel.Composition;  
    using System.Linq;  
    using System.Threading;  
    using Microsoft.VisualStudio.Text;  
    using Microsoft.VisualStudio.Text.Classification;  
    using Microsoft.VisualStudio.Text.Editor;  
    using Microsoft.VisualStudio.Text.Operations;  
    using Microsoft.VisualStudio.Text.Tagging;  
    using Microsoft.VisualStudio.Utilities;  
    using System.Windows.Media;  
    ```  
  
4.  Créez une classe qui hérite de <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> et nommez-le `HighlightWordTag`.  
  
    ```csharp  
    internal class HighlightWordTag : TextMarkerTag  
    {  
  
    }  
    ```  
  
5.  Créez une deuxième classe qui hérite de <xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition>et nommez-le HighlightWordFormatDefinition. Pour utiliser cette définition de format pour votre étiquette, vous devez l’exporter avec les attributs suivants :  
  
    -   <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: balises utilisent pour faire référence à ce format  
  
    -   <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>: cela entraîne le format s’affichent dans l’interface utilisateur  
  
    ```csharp  
  
    [Export(typeof(EditorFormatDefinition))]  
    [Name("MarkerFormatDefinition/HighlightWordFormatDefinition")]  
    [UserVisible(true)]  
    internal class HighlightWordFormatDefinition : MarkerFormatDefinition  
    {  
  
    }  
    ```  
  
6.  Dans le constructeur de HighlightWordFormatDefinition, définissez son nom d’affichage et l’apparence. La propriété d’arrière-plan définit la couleur de remplissage, alors que la propriété de premier plan définit la couleur de bordure.  
  
    ```csharp  
    public HighlightWordFormatDefinition()  
    {  
                this.BackgroundColor = Colors.LightBlue;  
        this.ForegroundColor = Colors.DarkBlue;  
        this.DisplayName = "Highlight Word";  
        this.ZOrder = 5;  
    }  
    ```  
  
7.  Dans le constructeur de HighlightWordTag, passer le nom de la définition de format que vous venez de créer.  
  
    ```  
    public HighlightWordTag() : base("MarkerFormatDefinition/HighlightWordFormatDefinition") { }  
    ```  
  
## <a name="implementing-an-itagger"></a>Implémentation d’un ITagger  
 L’étape suivante consiste à implémenter la <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> interface. Cette interface attribué, à la mémoire tampon de texte donné, les balises qui fournissent la mise en surbrillance de texte et les autres effets visuels.  
  
#### <a name="to-implement-a-tagger"></a>Pour implémenter un baliseur  
  
1.  Créez une classe qui implémente <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> de type `HighlightWordTag`et nommez-le `HighlightWordTagger`.  
  
    ```csharp  
    internal class HighlightWordTagger : ITagger<HighlightWordTag>  
    {  
  
    }  
    ```  
  
2.  Ajoutez les champs privés suivants et les propriétés à la classe :  
  
    -   Un <xref:Microsoft.VisualStudio.Text.Editor.ITextView>, qui correspond à l’affichage de texte actuel.  
  
    -   Un <xref:Microsoft.VisualStudio.Text.ITextBuffer>, qui correspond à la mémoire tampon de texte qui se trouve sous l’affichage de texte.  
  
    -   Un <xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService>, qui est utilisé pour rechercher du texte.  
  
    -   Un <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator>, qui a des méthodes de navigation dans les étendues de texte.  
  
    -   A <xref:Microsoft.VisualStudio.Text.NormalizedSnapshotSpanCollection>, qui contient l’ensemble de mots pour mettre en surbrillance.  
  
    -   A <xref:Microsoft.VisualStudio.Text.SnapshotSpan>, qui correspond au mot actuel.  
  
    -   A <xref:Microsoft.VisualStudio.Text.SnapshotPoint>, qui correspond à la position actuelle du point d’insertion.  
  
    -   Un objet de verrouillage.  
  
    ```csharp  
    ITextView View { get; set; }  
    ITextBuffer SourceBuffer { get; set; }  
    ITextSearchService TextSearchService { get; set; }  
    ITextStructureNavigator TextStructureNavigator { get; set; }  
    NormalizedSnapshotSpanCollection WordSpans { get; set; }  
    SnapshotSpan? CurrentWord { get; set; }  
    SnapshotPoint RequestedPoint { get; set; }  
    object updateLock = new object();  
  
    ```  
  
3.  Ajoutez un constructeur qui initialise les propriétés répertoriées précédemment et ajoute <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> et <xref:Microsoft.VisualStudio.Text.Editor.ITextCaret.PositionChanged> gestionnaires d’événements.  
  
    ```csharp  
    public HighlightWordTagger(ITextView view, ITextBuffer sourceBuffer, ITextSearchService textSearchService,  
    ITextStructureNavigator textStructureNavigator)  
    {  
        this.View = view;  
        this.SourceBuffer = sourceBuffer;  
        this.TextSearchService = textSearchService;  
        this.TextStructureNavigator = textStructureNavigator;  
        this.WordSpans = new NormalizedSnapshotSpanCollection();  
        this.CurrentWord = null;  
        this.View.Caret.PositionChanged += CaretPositionChanged;  
        this.View.LayoutChanged += ViewLayoutChanged;  
    }  
  
    ```  
  
4.  Les gestionnaires d’événements à l’appel du `UpdateAtCaretPosition` (méthode).  
  
    ```csharp  
    void ViewLayoutChanged(object sender, TextViewLayoutChangedEventArgs e)  
    {  
        // If a new snapshot wasn't generated, then skip this layout   
        if (e.NewSnapshot != e.OldSnapshot)  
        {  
            UpdateAtCaretPosition(View.Caret.Position);  
        }  
    }  
  
    void CaretPositionChanged(object sender, CaretPositionChangedEventArgs e)  
    {  
        UpdateAtCaretPosition(e.NewPosition);  
    }  
    ```  
  
5.  Vous devez également ajouter un `TagsChanged` événement qui sera appelée par la méthode de mise à jour.  
  
     [!code-csharp[VSSDKHighlightWordTest#10](../extensibility/codesnippet/CSharp/walkthrough-highlighting-text_1.cs)]
     [!code-vb[VSSDKHighlightWordTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-highlighting-text_1.vb)]  
  
6.  Le `UpdateAtCaretPosition()` méthode recherche chaque mot dans la mémoire tampon de texte qui est identique au mot où le curseur est positionné et construit une liste de <xref:Microsoft.VisualStudio.Text.SnapshotSpan> des objets qui correspondent aux occurrences du mot. Il appelle ensuite `SynchronousUpdate`, ce qui déclenche le `TagsChanged` événement.  
  
    ```csharp  
    void UpdateAtCaretPosition(CaretPosition caretPosition)  
    {  
        SnapshotPoint? point = caretPosition.Point.GetPoint(SourceBuffer, caretPosition.Affinity);  
  
        if (!point.HasValue)  
            return;  
  
        // If the new caret position is still within the current word (and on the same snapshot), we don't need to check it   
        if (CurrentWord.HasValue  
            && CurrentWord.Value.Snapshot == View.TextSnapshot  
            && point.Value >= CurrentWord.Value.Start  
            && point.Value <= CurrentWord.Value.End)  
        {  
            return;  
        }  
  
        RequestedPoint = point.Value;  
        UpdateWordAdornments();  
    }  
  
    void UpdateWordAdornments()  
    {  
        SnapshotPoint currentRequest = RequestedPoint;  
        List<SnapshotSpan> wordSpans = new List<SnapshotSpan>();  
        //Find all words in the buffer like the one the caret is on  
        TextExtent word = TextStructureNavigator.GetExtentOfWord(currentRequest);  
        bool foundWord = true;  
        //If we've selected something not worth highlighting, we might have missed a "word" by a little bit  
        if (!WordExtentIsValid(currentRequest, word))  
        {  
            //Before we retry, make sure it is worthwhile   
            if (word.Span.Start != currentRequest  
                 || currentRequest == currentRequest.GetContainingLine().Start  
                 || char.IsWhiteSpace((currentRequest - 1).GetChar()))  
            {  
                foundWord = false;  
            }  
            else  
            {  
                // Try again, one character previous.    
                //If the caret is at the end of a word, pick up the word.  
                word = TextStructureNavigator.GetExtentOfWord(currentRequest - 1);  
  
                //If the word still isn't valid, we're done   
                if (!WordExtentIsValid(currentRequest, word))  
                    foundWord = false;  
            }  
        }  
  
        if (!foundWord)  
        {  
            //If we couldn't find a word, clear out the existing markers  
            SynchronousUpdate(currentRequest, new NormalizedSnapshotSpanCollection(), null);  
            return;  
        }  
  
        SnapshotSpan currentWord = word.Span;  
        //If this is the current word, and the caret moved within a word, we're done.   
        if (CurrentWord.HasValue && currentWord == CurrentWord)  
            return;  
  
        //Find the new spans  
        FindData findData = new FindData(currentWord.GetText(), currentWord.Snapshot);  
        findData.FindOptions = FindOptions.WholeWord | FindOptions.MatchCase;  
  
        wordSpans.AddRange(TextSearchService.FindAll(findData));  
  
        //If another change hasn't happened, do a real update   
        if (currentRequest == RequestedPoint)  
            SynchronousUpdate(currentRequest, new NormalizedSnapshotSpanCollection(wordSpans), currentWord);  
    }  
    static bool WordExtentIsValid(SnapshotPoint currentRequest, TextExtent word)  
    {  
        return word.IsSignificant  
            && currentRequest.Snapshot.GetText(word.Span).Any(c => char.IsLetter(c));  
    }  
  
    ```  
  
7.  Le `SynchronousUpdate` effectue une mise à jour synchrone sur le `WordSpans` et `CurrentWord` propriétés et déclenche le `TagsChanged` événement.  
  
    ```vb  
    void SynchronousUpdate(SnapshotPoint currentRequest, NormalizedSnapshotSpanCollection newSpans, SnapshotSpan? newCurrentWord)  
    {  
        lock (updateLock)  
        {  
            if (currentRequest != RequestedPoint)  
                return;  
  
            WordSpans = newSpans;  
            CurrentWord = newCurrentWord;  
  
            var tempEvent = TagsChanged;  
            if (tempEvent != null)  
                tempEvent(this, new SnapshotSpanEventArgs(new SnapshotSpan(SourceBuffer.CurrentSnapshot, 0, SourceBuffer.CurrentSnapshot.Length)));  
        }  
    }  
    ```  
  
8.  Vous devez implémenter le <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> (méthode). Cette méthode accepte une collection de <xref:Microsoft.VisualStudio.Text.SnapshotSpan> objets et retourne une énumération des étendues de balises.  
  
     En c#, implémentez cette méthode comme un itérateur yield, qui permet l’évaluation tardive (autrement dit, l’évaluation du jeu uniquement lors de l’accès aux éléments individuels) des balises. En Visual Basic, ajoutez les étiquettes à une liste et retourner la liste.  
  
     Ici, la méthode retourne un <xref:Microsoft.VisualStudio.Text.Tagging.TagSpan%601> objet qui a une « blue » <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>, qui fournit un arrière-plan bleu.  
  
    ```csharp  
    public IEnumerable<ITagSpan<HighlightWordTag>> GetTags(NormalizedSnapshotSpanCollection spans)  
    {  
        if (CurrentWord == null)  
            yield break;  
  
        // Hold on to a "snapshot" of the word spans and current word, so that we maintain the same  
        // collection throughout  
        SnapshotSpan currentWord = CurrentWord.Value;  
        NormalizedSnapshotSpanCollection wordSpans = WordSpans;  
  
        if (spans.Count == 0 || wordSpans.Count == 0)  
            yield break;  
  
        // If the requested snapshot isn't the same as the one our words are on, translate our spans to the expected snapshot   
        if (spans[0].Snapshot != wordSpans[0].Snapshot)  
        {  
            wordSpans = new NormalizedSnapshotSpanCollection(  
                wordSpans.Select(span => span.TranslateTo(spans[0].Snapshot, SpanTrackingMode.EdgeExclusive)));  
  
            currentWord = currentWord.TranslateTo(spans[0].Snapshot, SpanTrackingMode.EdgeExclusive);  
        }  
  
        // First, yield back the word the cursor is under (if it overlaps)   
        // Note that we'll yield back the same word again in the wordspans collection;   
        // the duplication here is expected.   
        if (spans.OverlapsWith(new NormalizedSnapshotSpanCollection(currentWord)))  
            yield return new TagSpan<HighlightWordTag>(currentWord, new HighlightWordTag());  
  
        // Second, yield all the other words in the file   
        foreach (SnapshotSpan span in NormalizedSnapshotSpanCollection.Overlap(spans, wordSpans))  
        {  
            yield return new TagSpan<HighlightWordTag>(span, new HighlightWordTag());  
        }  
    }  
    ```  
  
## <a name="creating-a-tagger-provider"></a>Création d’un fournisseur de Baliseur  
 Pour créer votre balise, vous devez implémenter un <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider>. Cette classe est un composant MEF, vous devez donc définir les attributs appropriés afin que cette extension soit reconnue.  
  
> [!NOTE]
>  Pour plus d’informations sur MEF, consultez [Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index).  
  
#### <a name="to-create-a-tagger-provider"></a>Pour créer un fournisseur de baliseur  
  
1.  Créez une classe nommée `HighlightWordTaggerProvider` qui implémente <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider>et l’exporter avec un <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de « text » et un <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> de <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>.  
  
    ```csharp  
    [Export(typeof(IViewTaggerProvider))]  
    [ContentType("text")]  
    [TagType(typeof(TextMarkerTag))]  
    internal class HighlightWordTaggerProvider : IViewTaggerProvider  
    { }  
    ```  
  
2.  Vous devez importer les deux services de l’éditeur, le <xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService> et <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>, pour instancier la balise.  
  
    ```csharp  
    [Import]  
    internal ITextSearchService TextSearchService { get; set; }  
  
    [Import]  
    internal ITextStructureNavigatorSelectorService TextStructureNavigatorSelector { get; set; }  
  
    ```  
  
3.  Implémentez la <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A> méthode pour retourner une instance de `HighlightWordTagger`.  
  
    ```csharp  
    public ITagger<T> CreateTagger<T>(ITextView textView, ITextBuffer buffer) where T : ITag  
    {  
        //provide highlighting only on the top buffer   
        if (textView.TextBuffer != buffer)  
            return null;  
  
        ITextStructureNavigator textStructureNavigator =  
            TextStructureNavigatorSelector.GetTextStructureNavigator(buffer);  
  
        return new HighlightWordTagger(textView, buffer, TextSearchService, textStructureNavigator) as ITagger<T>;  
    }  
    ```  
  
## <a name="building-and-testing-the-code"></a>Création et test du code  
 Pour tester ce code, générez la solution HighlightWordTest et l’exécuter dans l’instance expérimentale.  
  
#### <a name="to-build-and-test-the-highlightwordtest-solution"></a>Pour générer et tester la solution HighlightWordTest  
  
1.  Générez la solution.  
  
2.  Lorsque vous exécutez ce projet dans le débogueur, une deuxième instance de Visual Studio est instanciée.  
  
3.  Créez un fichier texte et tapez du texte dans laquelle les mots sont répétés, par exemple, « hello hello hello ».  
  
4.  Placez le curseur dans un des occurrences de « hello ». Toutes les occurrences doivent être mis en surbrillance en bleu.  
  
## <a name="see-also"></a>Voir aussi  
 [Procédure pas à pas : Liaison d’un type de contenu à une extension de nom de fichier](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)