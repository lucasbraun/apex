# マイルストーンの改善

## 紹介
このラボでは、*対話グリッド* のレイアウトを更新して保存し、マイルストーンを改善する方法を学びます。

## タスク1: Name列を変更する
ランタイム環境で **マイルストーン**をクリックし、レコードをダブルクリックすると、詳細を編集できます。 各列に移動し、Project列が選択リスト、Name列とDescription列がテキストエリア、Due Date列が日付ピッカーであることに注意してください。 通常、Name列はそれほど長くありません。 これから列タイプをテキスト・フィールドに更新する必要があります。

1. アプリケーション・ビルダーに移動します。
2. アプリケーション内で、ページ・デザイナの**ページ5: マイルストーン**に移動します。
3. レンダリング・ツリー(左ペイン) で、**Project Milestones**リージョンの下にある**列**を展開します。
     列のリスト内で[**NAME**]をクリックします。
     プロパティ・エディター(右側のペイン) で、[識別] > [タイプ] で [**テキスト・フィールド**]を選択します。

    ![](images/set-name.png " ")

4. アプリケーション ツールバーで、**保存して実行**をクリックします。
     レコードをダブルクリックして、[Name] 列を確認します。

    ![](images/view-name.png " ")

## タスク2: グリッド レイアウトを更新する
もう一度レポートを見直して、Name、Project、Due Date、Descriptionの順に列を並べ替えると効果的です。 また、[Name] 列を固定して、ユーザーが左右にスクロールして [Description] 列をさらに表示できるようにすると便利です。

1. ランタイム環境で、[**アクション**]をクリックし、[**列**]をクリックします。

    ![](images/go-columns.png " ")

2. [列] ダイアログで [**Name**]をクリックし、上矢印をクリックして列を **プロジェクト** の前に移動します。
     **保存**をクリックします。

    ![](images/move-name.png " ")

3. ドラッグ アンド ドロップを使用して列を並べ替えることもできます。
       - 移動インジケータが表示されるまで、**Due Date** 列の先頭にカーソルを合わせます。
       - マウスをクリックしたままにします。
       - **Description** 列の前に表示されるまで、列を左にドラッグします。
       - マウスを放して列をドロップします。

    ![](images/show-movement.png " ")
    ![](images/drag-date.png " ")

4. グリッドを見やすくするために、メニューを折りたたむことができます。
     アプリケーション名の前にあるアイコンをクリックします。

    ![](images/hide-menu.png " ")

5. 列が正しい順序になったので、名前列を固定する必要があります。
       - **Name**の列見出しをクリックします。
       - **固定**をクリックします。

    ![](images/freeze.png " ")

6. データをより適切に表示するには、列のサイズを調整する必要があります。
    - サイズ変更インジケーターが表示されるまで、**Name** 列と **Project** 列の間にカーソルを置きます。
    - **Name** 列に適したサイズになるまで、列区切りを右にドラッグします。
    - **Project** 列と **Due Date** 列についても繰り返します。   
     *注意: 列の末尾にあるサイズ変更インジケーターを使用して、[説明] 列のサイズを拡大することもできます*

    ![](images/get-resize.png " ")
    ![](images/column-sizes.png " ")

7. フリーズ表示をテストするには、メニューを再表示します。 アプリケーション名の前にあるアイコンをクリックします。

    ![](images/freeze-display.png " ")

## タスク3: レポートを保存する
グリッド・レイアウトに加えた変更は、自分だけに表示されます。 他のユーザーがログインすると、以前の列の順序と列のサイズで元のレイアウトが表示されます。 これからデフォルトのレポート レイアウトを保存する必要があります。

1. ランタイム環境で、[アクション]をクリックし、[レポート]を選択してから、[保存]を選択します。   
     *注意: アプリケーション・ビルダー からアプリケーションを実行した開発者のみが、デフォルト・レポートを保存できます。 エンド ユーザーは [別名保存] のみを使用できます*

    ![](images/save.png " ")

## **まとめ**

これでラボ6は終了です。これで、対話グリッドを操作してデフォルトレポートを保存する方法がわかりました。 [ラボ7に移動するには、ここをクリックしてください](?lab=lab-7-improving-tasks)

## **謝辞**

  - **著者** - Salim Hlayel, Principle Product Manager
  - **寄稿者** - Arabella Yao, Product Manager Intern, DB Product Management
  - **最終更新者/日付** - Madhusudhan Rao, Apr 2022
