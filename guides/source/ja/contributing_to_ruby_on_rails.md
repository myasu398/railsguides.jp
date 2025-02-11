Ruby on Rails に貢献する方法
=============================

本ガイドでは、Ruby on Railsの開発に「あなた」が参加する方法について説明します。

このガイドの内容:

* GitHubでissueをレポートする方法
* マスターをcloneしてテストスイートを実行する方法
* 既存のissueを解決する方法
* Ruby on Railsのドキュメントに貢献する方法
* Ruby on Railsのコードに貢献する方法

Ruby on Railsは、「どこかで誰かがうまくやってくれているフレームワーク」ではありません。Ruby on Railsには、長年に渡って数千人もの人々が貴重な貢献を行ってくださいました。その内容は、わずか1文字の修正から、大規模なアーキテクチャ変更、重要なドキュメント作成まで多岐に渡ります。それらの努力は、いずれもRuby on Railsをすべての人々にとってよりよいものにすることを目標に置いています。コードを書いたりドキュメントを作成したりするまでには至らなくても、issueのレポートやパッチのテストなど、さまざまな方法で貢献することができます (訳注: **サンプルの文章も日本語に翻訳されていますが、実際には必ず英語を使うようにしてください** )。

[RailsのREADME](https://github.com/rails/rails/blob/master/README.md)にも記載されているように、Railsのコードベースやサブプロジェクトのコードベースについて、issueトラッカーやチャットルームやメーリングリストでやり取りする方は誰であっても、Railsの[行動規範](https://rubyonrails.org/conduct/)に従うことが期待されます。

--------------------------------------------------------------------------------


issueのレポート
------------------

Ruby on Railsでは[GitHubのIssueトラッキング](https://github.com/rails/rails/issues)機能でissueをトラッキングしています。主にバグや、新しいコードの貢献に使用されます。Ruby on Railsでバグを見つけたら、そこから貢献を開始できます。GitHubへのissue送信、コメント、プルリクエストの作成を行うには、まずGitHubアカウント (無料) を作成する必要があります。

NOTE: Ruby on Railsの最新リリースで見つけたバグは最も注目を集める可能性があります。また、Railsコアチームは、_edge Rails_ (その時点での開発版Railsのコード) でのテストに時間を割いてくれる方からのフィードバックを常に歓迎しています。テスティング用にedge Railsを入手する方法については後述します。

### バグレポートを作成する

Ruby on Railsで何らかの問題を発見し、それがセキュリティ上の問題でなければ、まずGitHubの[issue](https://github.com/rails/rails/issues)を検索して、既にレポートがあがっているかどうかを確認してみましょう。該当する問題がissuesにまだ挙がっていない場合は、[新しいissueを作成](https://github.com/rails/rails/issues/new)します。セキュリティ上のissueをレポートする方法については次のセクションで説明します。

issueレポートには、最低でもタイトルとissueの明快な説明が必要です。できるだけ多くの関連情報を含めるようにしてください。また、少なくとも問題を再現できるコードサンプルも合わせて投稿してください。期待される動作が行われていないことを示す単体テストも含めてもらえるとさらに助かります。バグの再現と修正点の把握を、他の人達にとっても自分自身にとってもやりやすくすることを目指してください。

そして、issueの扱いについて過度な期待を抱かないことも肝心です。「地球滅亡クラス」の重大な問題でもない限り、レポートしてもらったissueは他のissueと同様に、解決に向けて共同作業が行われるようになります。issueレポートが自動的に修正担当者を見つけてくれることもありませんし、他の開発者が自分の作業を差し置いてまで修正してくれることもありません。issueを作成するということはほとんどの場合、自分にとっては問題修正のスタートラインに着くことであり、他の開発者にとっては「こちらでも同じ問題が起きてます」と確認およびコメントを追加する場所ができたということに過ぎません。

### 実行可能なテストケースを作成する

自分のissueを再現する方法を用意することは、他の開発者がissueを確認、調査、そして修正する上で大変役立ちます。そのための方法は、実行可能なテストケースを提供することです。この作業を少しでも簡単にするために、Railsチームはバグレポートのテンプレートを多数用意しています。これを元に作業を開始できます。

* Active Record (モデル、データベース) issue用テンプレート: [gem](https://github.com/rails/rails/blob/master/guides/bug_report_templates/active_record_gem.rb) / [master](https://github.com/rails/rails/blob/master/guides/bug_report_templates/active_record_master.rb)
* Action Pack (コントローラ、ルーティング) issue用テンプレート: [gem](https://github.com/rails/rails/blob/master/guides/bug_report_templates/action_controller_gem.rb) / [master](https://github.com/rails/rails/blob/master/guides/bug_report_templates/action_controller_master.rb)
* その他の一般的なissue用テンプレート: [gem](https://github.com/rails/rails/blob/master/guides/bug_report_templates/generic_gem.rb) / [master](https://github.com/rails/rails/blob/master/guides/bug_report_templates/generic_master.rb)

テンプレートには「ボイラープレート(boilerplate)」と呼ばれる一種のひな形コードが含まれており、これを使用してRailsのリリースバージョン(`*_gem.rb`)やedge Rails (`*_master.rb`)に対するテストケースを設定することができます。

該当するテンプレートの内容をコピーして`.rb`ファイルに貼り付けて適宜変更を行い、issueを再現できるようにします。このコードを実行するには、ターミナルで`ruby the_file.rb`を実行します。テストコードが正しく作成されていれば、このテストケースはバグがあることによって失敗する (failと表示される) はずです。

続いて、この実行可能テストケースをGitHubの[gist](https://gist.github.com)で共有するか、issueの説明に貼り付けます。

### セキュリティissueの特殊な取り扱い方法について

WARNING: セキュリティ脆弱性に関する問題は、一般公開されているGitHubのissueレポート機能には「絶対に掲載しないでください」。セキュリティ関連のissueを扱う方法の詳細については、[Railsセキュリティポリシーページ](https://rubyonrails.org/security) (英語) を参照してください。

### 機能リクエストについて

GitHubのIssueには「機能リクエスト」を記入しないでください。Ruby on Railsで欲しい機能があるなら、自分でコードを書いてください。あるいは、誰かにお願いしてコードを書いてもらってください。Ruby on Rails用のパッチを提案する方法については後述します。たとえGitHubのissueにこのような「欲しい機能リスト」をコードも添えずに書き込んだところで、Issueをチェックした人によって早晩「無効」とマーキングされて終わるでしょう。

その一方、「バグ」と「機能」の線引きはそう簡単ではないこともあります。一般に、「機能」はアプリケーションに新しい振る舞いを追加するものであり、バグとは既存の振る舞いが期待どおりでないことを示します。コアチームは、必要に応じてバグか機能かを審査するための招集をかけることもあります。とはいうものの、バグか機能かの違いは、送っていただいたパッチを (ボツにするかどうかというよりは)、どのリリースに反映するかという扱いの違いでしかないことがほとんどです。バグ修正は早めにリリースされ、機能追加は大きなリリース変更のときに反映されるといった具合です。私たちは、修正パッチと同様に機能追加も大歓迎しています。送っていただいた機能追加をメンテナンス用ブランチに押し込めておしまい、というようなことはしていません。

機能追加用のパッチを送信する前に自分のアイディアに意見を募りたい場合は、[rails-coreメーリングリスト](https://groups.google.com/forum/?fromgroups#!forum/rubyonrails-core)にメールを送信してください。もし誰からも返信がなければ、自分のアイディアに誰も関心を持っていないということがわかります。あるいは、自分のアイディアに興味を示してくれる人が返信してくれるかもしれません。あるいは「悪いけどそれは採用できそうにないね」という返信かもしれません。しかしこのメーリングリストは、こうしたアイディアについて議論するために用意された場所です。逆にGitHubのissueは、こうした新しいアイディアのために必要な議論 (ときには長期かつ複雑になることもあるでしょう) を行うための場所ではありません。


既存のissueの解決を手伝う
----------------------------------

issueのレポートの次の段階となる貢献方法として、既存のissueにフィードバックすることでコアチームによるissue解決を手伝うこともできます。Railsのコア開発経験がない方にとってはまたとない初期の貢献となるでしょうし、Railsのコードベースや問題解決の手順に親しむチャンスにもなります。

GitHubのissueにあがっている[issueのリスト] (https://github.com/rails/rails/issues)を見てみると、注目を集めているissueがたくさん見つかります。自分も何かissueに貢献できる方法はあるでしょうか。もちろんあります。それもいろんな方法があります。

### バグレポートの確認

初歩的な貢献として、バグレポートを確認する作業も大変役に立ちます。issueを自分のコンピュータで再現できるかどうかを試してみましょう。問題をうまく再現できたら、そのことをissueのコメントに追加しましょう。

再現手順などにあいまいな点があるなら、どこがわかりにくいかを指摘しましょう。バグを再現するために有用な情報を追加したり、不要な手順を削除したりするのも重要な貢献です。

テストが添えられていないバグレポートを見かけたら、貢献のチャンスです。ソースコードを追いかける絶好の機会にもなります。バグが原因で失敗するテストを作成して貢献できます。テストの書き方は、既存のテストファイルを詳しく読むことで学べます。これは、Railsのソースコードをみっちり探索するためのよいきっかけにもなります。作成するテストは「パッチ」の形式にしてもらえるとベストです。詳しくは[Railsのコードに貢献する](/contributing_to_ruby_on_rails.html#rails%E3%81%AE%E3%82%B3%E3%83%BC%E3%83%89%E3%81%AB%E8%B2%A2%E7%8C%AE%E3%81%99%E3%82%8B)で後述します。

バグレポートは、とにかく簡潔でわかりやすく、そしてなるべく簡単に現象を再現できるように書いてください。バグを修正する開発者にとって何よりありがたいのは、このような「よいバグレポート」です。たとえバグレポートを作成するあなたが最終的にコードを書かなくても、よいバグレポートは大きな貢献となります。

### パッチをテストする

GitHubからRuby on Railsに送信されたプルリクエスト (pull request、プルリクとも) をチェックしてくれる人もいると助かります。寄せられた修正を適用するには、まず次のように専用のブランチを作成してください。

```bash
$ git checkout -b testing_branch
```

続いて、このリモートブランチを使用してローカルのコードベースを更新します。たとえばGitHubユーザーであるJohnSmithが、forkして https://github.com/JohnSmith/rails の"orange"というトピックブランチにpushしたとします。

```bash
$ git remote add JohnSmith https://github.com/JohnSmith/rails.git
$ git pull JohnSmith orange
```

ブランチを適用したらテストしてみます。次のような点に注意しながら進めましょう。

* 修正は本当に有効か。
* このテストで自分は幸せになれるか。何がテストされているのかを自分が理解できているか。足りないテストはないか。
* ドキュメントに適切な記載があるか。ドキュメントも更新する必要があるか。
* 実装が楽しいと思えるか。同じ変更をもっと高速かつ素晴らしい方法で実装する方法を思い付けるか。

プルリクエストに含まれている変更点がよいものであると思えたら、GitHubのissueに賛成を表明(approval)するコメントを追加してください。追加するコメントでは、まずその変更に賛成していることを表明しつつ、なるべく具体的にどの変更点がよいと思ったのかについても示しましょう。たとえば次のようにコメントします。

>I like the way you've restructured that code in generate_finder_sql - much nicer. (generate_finder_sqlのコードが非常によい形で再構築されている点がよいと思います)。The tests look good too. (テストもよく書けているようです)。

単に「+1」とありがちなコメントを残すだけでは、他のレビュアーはほとんど注目してくれないでしょう。コメントするあなたが十分時間をかけてプルリクエストを読んだということが皆に伝わるように書きましょう。

Railsのドキュメントに貢献する
---------------------------------------

Ruby on Railsには2種類のドキュメントがあります。ひとつはこのガイドであり、Ruby on Railsを学ぶためのものです。もうひとつはAPIドキュメントであり、こちらはリファレンス用です。

どなたでもRailsガイドの改善に貢献することができます。Railsガイドに求められる改善とは、「一貫していること」「矛盾がないこと」「読みやすいこと」「情報の追加」「事実と異なっている部分の修正」「タイポの修正」「最新のedge Railsに追い付くこと」などです。

英語ドキュメントに貢献したい方は、Railsガイドの[英語ソースファイル](https://github.com/rails/rails/tree/master/guides/source)を変更してから、プルリクエストでmasterブランチに変更の反映を依頼してください。

ドキュメント関連で貢献したい場合は、[API ドキュメント作成のガイドライン](api_documentation_guidelines.html) と[Rails ガイドのガイドライン](ruby_on_rails_guides_guidelines.html) をよく読んでからにしてください。

NOTE: RailsのCI (継続的インテグレーション: Continuous Integration) サーバーの負荷を減らすために、ドキュメント関連のコミットメッセージには[ci skip]と記入してください。こうすることで、コミット時のビルドはスキップされます。[ci skip] は「ドキュメントのみの変更」以外では使用できません。コードの変更には絶対使用しないでください。

Railsガイドの翻訳に貢献する
------------------------

Railsガイドを翻訳してくださるボランティアも歓迎いたします。次の手順に沿ってください。

* https://github.com/rails/rails をforkします。
* 翻訳先の言語名に対応するフォルダをsourceフォルダの下に追加します。たとえば、イタリア語であればguides/source/it-ITフォルダを追加します。
* *guides/source*に置かれているコンテンツファイルをそのフォルダ内にコピーして翻訳します。
* HTMLファイルは**翻訳しないでください**（自動生成されます）。

翻訳の送り先はRailsリポジトリではないことにご注意ください。上述したように、翻訳はforkしたリポジトリで行います。ドキュメントのメンテナンスをパッチベースで行う場合、英語のみに統一しておかないと維持できないためです。

ガイドをHTML形式で生成するには、guidesディレクトリに`cd`して以下を実行します（言語がit-ITの場合）。

```bash
$ bundle install
$ bundle exec rake guides:generate:html GUIDES_LANGUAGE=it-IT
```

これにより、outputディレクトリにガイドが生成されます。

NOTE: 上述の手順はRails 5以降が対象です。redcarpet gemはJRubyでは動きません。

現在把握されている翻訳プロジェクトは以下のとおりです（バージョンはそれぞれ異なっています）。

* **イタリア語**: [https://github.com/rixlabs/docrails](https://github.com/rixlabs/docrails)
* **スペイン語**: [https://github.com/gramos/docrails/wiki](https://github.com/gramos/docrails/wiki)
* **ポーランド語**: [https://github.com/apohllo/docrails](https://github.com/apohllo/docrails)
* **フランス語** : [https://github.com/railsfrance/docrails](https://github.com/railsfrance/docrails)
* **チェコ語** : [https://github.com/rubyonrails-cz/docrails/tree/czech](https://github.com/rubyonrails-cz/docrails/tree/czech)
* **トルコ語** : [https://github.com/ujk/docrails](https://github.com/ujk/docrails)
* **韓国語** : [https://github.com/rorlakr/rails-guides](https://github.com/rorlakr/rails-guides)
* **中国語（簡体字）** : [https://github.com/ruby-china/guides](https://github.com/ruby-china/guides)
* **中国語（繁体字）** : [https://github.com/docrails-tw/guides](https://github.com/docrails-tw/guides)
* **ロシア語** : [https://github.com/morsbox/rusrails](https://github.com/morsbox/rusrails)
* **日本語** : [https://github.com/yasslab/railsguides.jp](https://github.com/yasslab/railsguides.jp)

Railsのコードに貢献する
------------------------------

### development環境を構築する

バグレポートを送信して既存の問題解決を手伝ったり、コードを書いてRuby on Railsに貢献したりするためには、ぜひともテストスイートを実行できるようにしておく必要があります。このセクションでは、自分のパソコン上でテスト用の環境を構築する方法について解説します。

#### 楽な方法

[rails-dev-box](https://github.com/rails/rails-dev-box)にあるできあいのdevelopment環境を入手するのがおすすめです。

#### 面倒な方法

Rails development boxを利用できない事情がある場合は、Railsガイドの[Railsコア開発環境の構築方法](development_dependencies_install.html)をご覧ください。

### Railsリポジトリをクローンする

コードに貢献するには、まずRailsリポジトリをクローンするところから始める必要があります。

```bash
$ git clone https://github.com/rails/rails.git
```

続いて、専用のブランチを作成します。

```bash
$ cd rails
$ git checkout -b my_new_branch
```

このブランチの名前はローカルコンピュータの自分のリポジトリ上でしか使われないので、どんな名前でも構いません。この名前がRails Gitリポジトリにそのまま取り込まれることはありません。

### Bundle install

必要なgemをインストールします。

```bash
$ bundle install
```

### ローカルブランチでアプリケーションを実行する

ダミーのRailsアプリケーションで変更をテストする必要がある場合は、`rails new`に`--dev`フラグを追加すると、ローカルブランチを使用するアプリケーションが生成されます。

```bash
$ cd rails
$ bundle exec rails new ~/my-test-app --dev
```

`~/my-test-app`で生成されたアプリケーションはローカルブランチのコードを実行します。サーバーを再起動すると、設定の変更をアプリケーションで確認できます。

### コードを書く

体制が整ったので、早速コードを追加・編集しましょう。現在のGitブランチで存分にコードを書くことができます (念のため`git branch -a`を実行して、正しいブランチにいることを確認しておきましょう)。自分のコードをRailsに追加するのであれば、以下の点を心がけてください。

* 正しいコードを書くこと。
* Railsで皆が使用している慣例やヘルパーメソッドを使用すること。
* テストを書くこと。自分のコードがないと失敗し、あると成功するテストであること。
* 関連するドキュメント、実行例、ガイドなど、コードが影響する部分はすべて更新すること。


TIP: 表面的なものにとどまる変更や、Railsの安定性/機能性/テストのしやすさの根本的な部分を何も改良しないような変更は受け付けられません。詳細については [our rationales behind this decision](https://github.com/rails/rails/pull/13771#issuecomment-32746700) (英語) を参照してください。

#### Railsコーディングルールに従う

Railsのコーディングを行う場合は、以下のシンプルなスタイルガイドに従います。

* インデントはスペース2つを使用する。タブ文字は使用しないこと。
* 行末にスペースを置かないこと。空行に余分なスペースを置かないこと。
* privateやprotectedの直後の行は空行にせず、以降の行をインデントする。
* ハッシュの記法は Ruby 1.9 以降の書式を使用する。つまり「`{ :a => :b }`」よりも「`{ a: :b }`」が望ましい。
* 「`and`/`or`」よりも「`&&`/`||`」が望ましい。
* クラスメソッドは「self.method」よりも「class << self」が望ましい。
* 引数の記述はかっこ+スペース「`my_method( my_arg )`」やかっこなし「`my_method my_arg`」ではなく、スペース無しかっこ「`my_method(my_arg)`」を使用すること。
* 等号の前後にはスペースを置く。「`a=b`」ではなく「`a = b`」とすること。
* refuteではなくassert\_notを使用すること。
* 単一行ブロックはスペース無しの「`method{do_stuff}`」よりもスペースありの「`method { do_stuff }`」が望ましい。
* その他、Railsのコードにある既存の書式に従うこと。

上はあくまでガイドラインであり、最適な使用方法については各自でご判断ください。

その他に、私たちのコーディング規約の一部をコード化するために定義された[RuboCop](https://www.rubocop.org/)ルールも用いています。プルリクエストを送信する前に、ローカルで変更をかけたファイルに対してRuboCopを実行してください。

```bash
$ rubocop actionpack/lib/action_controller/metal/strong_parameters.rb
Inspecting 1 file
.
1 file inspected, no offenses detected
```


`rails-ujs`のCoffeeScriptやJavaScriptファイルについては、`actionview`フォルダで`npm run lint`を実行できます。

### ベンチマークを行う

パフォーマンスに影響する可能性のある変更をかけるばあいは、コードのベンチマークを取って影響の大きさを測定するようお願いします。その際、使ったベンチマークスクリプトも結果に添えてください。コミットメッセージにもその旨を明記し、今後別のコントリビューターが必要に応じてその結果をすぐ見つけて検証したり決定を下したりできるようにしましょう（たとえば、今後Ruby VMの最適化が行われれば、現在の最適化の一部が不要になるということも考えられます）。

特定の状況に限ってパフォーマンスを改善するなら非常に簡単に最適化できますが、他の多くの状況ではパフォーマンス低下が再発するでしょう。したがって、代表的な状況を網羅したリストに対して変更をテストすべきです。理想的には、productionアプリケーションから得た現実的なシナリオに基づくべきです。

[ベンチマーク用のテンプレート](https://github.com/rails/rails/blob/master/guides/bug_report_templates/benchmark.rb)を元にするとよいでしょう。このテンプレートには、[benchmark-ips](https://github.com/evanphx/benchmark-ips) gemを用いてベンチマークを設定するコードテンプレートが含まれており、スクリプト内にインライン記述できるような比較的自己完結的なテストを念頭に設計されています。

### テストを実行する

Railsでは、変更をプッシュする時にテストスイートをフル実行するという慣習があるわけではありません。おすすめのワークフーロー[rails-dev-box](https://github.com/rails/rails-dev-box)で説明しているように、railtiesのテストは特に時間がかかり、ソースコードを`/vagrant`にマウントするとさらに時間がかかります。

現実的な妥協案として、作成したコードによって影響が生じるかどうかをテストするようにしてください。そして、変更がrailtiesで行われていないのであれば、影響を受けるコンポーネントのすべてのテストスイートを実行してください。テストにすべてパスすれば、貢献を提案する準備が整います。Rails では、他の箇所で予想外のエラーが生じたときに検出できるよう、[Buildkite](https://buildkite.com/rails/rails)を使用しています。

#### Rails 全体のテストを実行する

すべてのテストを実行するには以下のようにします。

```bash
$ cd rails
$ bundle exec rake test
```

#### 特定のコンポーネントのテストを実行する

Action Packなど、特定のコンポーネントのテストのみを実行することもできます。たとえば、Action Mailerの場合は以下を実行します。

```bash
$ cd actionmailer
$ bundle exec rake test
```

#### 単一のテストを実行する

Rubyで単一のテストを実行することができます。たとえば次のようになります。

```bash
$ cd actionmailer
$ ruby -w -Itest test/mail_layout_test.rb -n test_explicit_class_layout
```

`-n`オプションを指定すると、ファイル全体ではなく指定した単一のメソッドだけを実行します。


#### 特定のseedでテストを実行する

テストの実行はseedでランダム化されます。テストがランダムに失敗する場合、ランダム化用のseedを指定することで、失敗するテストをより正確に再現できます。

あるコンポーネントのテストをすべて実行するには、以下のようにします。

```bash
$ cd actionmailer
$ SEED=15002 bundle exec rake test
```

特定のテストファイル1件を実行する場合は以下のようにします。

```bash
$ cd actionmailer
$ SEED=15002 bundle exec ruby -w -Itest test/mail_layout_test.rb
```

#### Active Recordをテストする

最初に、必要なデータベースを作成します。MySQLやPostgreSQLを使用するのであれば、SQL文「`create database activerecord_unittest`」と「`create database activerecord_unittest2`」で十分です。SQLite3の場合は不要です。

以下の手順で、SQLite3のみを対象にActive Recordのテストを実行します。

```bash
$ cd activerecord
$ bundle exec rake test:sqlite3
```

`sqlite3`のときと同様に、以下の手順で各アダプターを対象にテストを実行することができます。タスクはそれぞれ以下のようになります。

```bash
test:mysql2
test:postgresql
```

最後に以下を実行します。

```bash
$ bundle exec rake test
```

これで3つが順に実行されます。

単一のテストを個別に実行することもできます。

```bash
$ ARCONN=sqlite3 bundle exec ruby -Itest test/cases/associations/has_many_associations_test.rb
```

ひとつのテストをすべてのアダプターに対して実行するには以下のようにします。

```bash
$ bundle exec rake TEST=test/cases/associations/has_many_associations_test.rb
```

これで`test_jdbcmysql`、`test_jdbcsqlite3`、`test_jdbcpostgresql`も呼び出されます。特定のデータベーステストにターゲットを絞って実行する方法の詳細については`activerecord/RUNNING_UNIT_TESTS.rdoc`を参照してください。より多くのデータベースを対象にテストスイートを実行する方法について詳しくは、`activerecord/RUNNING_UNIT_TESTS.rdoc`を参照してください。

### 警告

テストスイートの実行では、警告表示がオンになります。Ruby on Railsのテストで警告がひとつも表示されないのが理想ですが、サードパーティのものも含めて若干の警告が表示されてしまうことがあります。無視するという手もありますが、可能であれば修正をお願いします。そしてできれば、新しい警告を表示しないようにするためのパッチの送信もお願いします。

### CHANGELOGの更新

CHANGELOGはすべてのリリースで重要な位置を占めます。Railsの各バージョンの変更点をここに記録します。

機能の追加や削除、バグ修正のコミット、非推奨通知の追加を行ったら、必ず修正したフレームワークのCHANGELOGの**冒頭に**エントリを追加してください。リファクタリングやドキュメント変更の場合はCHANGELOGを変更しないでください。

CHANGELOGのエントリには変更内容を的確に要約したものを記入し、最後に作者の名前を書きます。必要であれば複数行にわたってエントリを記入したり、スペース4つのインデントを置いたコード例を記入したりすることもできます。変更が特定のissueに関連する場合は、issue番号も記入してください。CHANGELOGエントリの例を以下に示します ( **訳注: 実際は英語で書きます** )。

```
*  (変更内容の要約を記入します)(複数行の
    エントリを記入する場合は80文字目で折り返します)(必要に応じてインデント付きのコード例を追加できます)

        class Foo
          def bar
            puts 'baz'
          end
        end

    （コード例に続けてエントリを書くこともできます。issue番号は「Fixes #1234」などと書きます）

    *自分の名前*
```

コード例や複数行エントリを使用しない場合、名前はエントリの最後に続けて記入してエントリを1行に収めてください。その他の場合は、最後の行に名前だけを記入してください。

### Gemfile.lockを更新する

変更内容によっては、依存関係もアップグレードしなければならないことがあります。そのような場合は、`bundle update` を実行して正しい依存関係バージョンを反映し、変更の`Gemfile.lock`ファイルにコミットしてください。

### 変更をコミットする

自分のPC上のコードに満足がいくようになったら、変更をGitにコミットします。

```bash
$ git commit -a
```

上を実行すると、コミットメッセージを作成するためのエディタが開きます。メッセージを作成したら保存して続行します。

コミットメッセージの書式をきちんと整え、わかりやすく記述してもらえると、他のメンバーが変更内容を理解する上で大変助かります。コミットメッセージは十分時間をかけて書いてください。

よいコミットメッセージは以下のような感じになります。

```
短い要約文 (50 文字以下だと理想的)

もちろん、必要であればもっと詳しく書いてください。メッセージは72文字目で改行してください。メッセージはできるだけ詳しく書くようにします。コミット内容が自明に思えるとしても、他の人にとってもそうであるとは限りません。関連する issue で言及されている記述もすべて追加し、履歴を探しにいかなくても良いようにすべきです。

記述は複数のパラグラフにわたってもかまいません。

コード例を記述に埋め込む際は、4つのスペースでインデントしてください。

    class ArticlesController
      def index
        render json: Article.limit(10)
      end
    end

箇条書きの点を追加することもできます。

- 箇条書きはダッシュ (-) または
 アスタリスク (*) で始めます

- 行は72文字目で折り返し、読みやすさのために
  追加行の冒頭にスペース2つを置いてインデントします
```

TIP: コミットが複数にわたっている場合は、必ず 1 つのコミットにスカッシュ(squash)しておいてください。これにより、今後のcherry pickがやりやすくなり、Gitのログも煩雑にならずに済みます。

### ブランチを更新する

ローカルで作業している間に、masterで別の更新が行われているということがよくあります。更新をローカルに取り込みましょう。

```bash
$ git checkout master
$ git pull --rebase
```

続いて、最新の変更のトップにパッチを再度適用しましょう。

```bash
$ git checkout my_new_branch
$ git rebase master
```

コンフリクトは生じなかったか、テストはパスするか、取り込んだ変更は納得できる内容か。それらを確認してから次に進みましょう。

### フォーク

Rails [GitHubリポジトリ](https://github.com/rails/rails) を開いて、右上隅にある [Fork] を押します。

ローカルPC上のローカルリポジトリに新しいリモートを追加します。

```bash
$ git remote add fork https://github.com/<自分のユーザー名>/rails.git
```

ローカルリポジトリは、オリジナルのrails/railsリポジトリからローカルリポジトリに`clone`して作ることも、自分のリポジトリにフォークしたものをローカルリポジトリに`clone`して作ることもできます。曖昧さを避けるため、以降のgitコマンドでは、rails/railsを指す`remote`コマンドを実行したと仮定します。

```bash
$ git remote add rails https://github.com/rails/rails.git
```

Railsの公式リポジトリから新しいコミットとブランチをダウンロードします。

```bash
$ git fetch rails
```

ダウンロードした新しいコンテンツをマージします。

```bash
$ git checkout master
$ git rebase rails/master
$ git checkout my_new_branch
$ git rebase rails/master
```

フォークをアップデートします。

```bash
$ git push fork master
$ git push fork my_new_branch
```


### プルリクエストを発行する

プッシュしたRailsアプリケーションのリポジトリを開いて (ここではhttps://github.com/your-user-name/rails にあるとします)、右ペインにある [Pull Requests] をクリックします。次のページで右上隅の [New pull request] を押します。

比較対象のブランチを変更したい場合は [Edit] をクリックし、(デフォルトではmasterが比較対象になります)。[Click to create a pull request for this comparison] をクリックします。

自分が導入した変更セットが含まれていることを確認します。送信したいパッチの詳細を記入し、わかりやすいタイトルを付けます。終わったら、[Send pull request] を押します。送信したプルリクエストはRailsコアチームに知らされます。

### フィードバックを受け取る

送信したプルリクエストがマージされるまでには、何回か再挑戦が必要になるでしょう。あなたのプルリクエストに対して別の意見を持つコントリビュータがいるかもしれません。多くの場合、プルリクエストがマージされるまでにパッチを何度か更新する必要もあるでしょう。

GitHubのメール通知機能をオンにしているRailsコントリビュータもいますが、そうでない人もいます。Railsに携わっている人のほとんどはボランティアなので、プルリクエストに何らかの反応が生じるまでに数日かかることもざらにあります。どうかめげずにプルリクエストをどしどし送信してください。びっくりするほど早く反応がもらえることもあれば、そうでないこともあります。それがオープンソースというものです。

一週間経っても何の音沙汰もないようなら、少しつっついてみましょう。[rubyonrails-coreメーリングリスト](https://groups.google.com/forum/#!forum/rubyonrails-core)をご利用ください。プルリクエストに自分でコメントを追加してみてもよいでしょう。

せっかくなので、自分のプルリクエストへの反応を待っている間に、他の人のプルリクエストを開いてコメントしてみましょう。あなたのパッチに反応があったときとおなじぐらい、その人たちもきっと嬉しく思うことでしょう。

### 必要なら何度でもトライする

Railsに貢献すべく活動していれば、そのプルリクエストはここを変えた方がよいのではないかというフィードバックを受けることがきっと一度や二度あるでしょう。そういうことがあっても、どうか落ち込まないでください。オープンソースプロジェクトに貢献するうえで肝心なのは、コミュニティの知恵を遠慮なく活用させてもらうことです。コミュニティのメンバーがあなたのコードの調整を求めているのであれば、そのとおりにして再送信する価値があります。そのコードはRailsのコアにおくべきではないというフィードバックを受けたなら、gemの形でリリースする方がよいかもしれません。

#### コミットをスカッシュする

Railsに貢献する皆様にお願いしたいのは、「コミットのスカッシュ」です。スカッシュ（squash）とは、複数のコミットをひとつにまとめることです (訳注: 後述の`git rebase -i`でスカッシュできます)。プルリクエストは、ひとつのコミットにまとめておくことが望まれます。コミットをひとつにまとめることで、安定版ブランチに新しい変更をバックポートしやすくなり、よくないコミットを取り消しやすくなり、Gitの履歴を多少なりとも追いやすくなります。Railsは巨大プロジェクトであり、異質なコミットが多数加わると膨大なノイズが生じる可能性があります。

```bash
$ git fetch rails
$ git checkout my_new_branch
$ git rebase -i rails/master

< 最初のひとつを除くすべてのコミットに対して'squash'を選択する >
< コミットメッセージを編集して、すべての変更をわかりやすく記述する >

$ git push fork my_new_branch --force-with-lease
```

以上でGitHub上のプルリクエストを更新できるようになり、実際に更新されたことを確認できます。

#### プルリクエストを更新する

あなたがコミットしたコードに対して変更を求められることがあります。既存のコミットそのものを修正することを求められることもあります。ただし、Gitでは既存のコミットをさかのぼって変更したものをプッシュすることは許されていません。既にプッシュされたブランチとローカルのブランチが一致しないからです。このような場合は、新しいプルリクエストを作成する代わりに、コミットのスカッシュについて既に説明した方法を使用して、自分のブランチをGitHubに強制的にプッシュすることもできます。

```bash
$ git push fork my_new_branch --force-with-lease
```

これにより、GitHub上のブランチとプルリクエストが新しいコードによって更新されます。強制的にプッシュを行うと、リモートブランチのコミットが失われる危険性がありますので、くれぐれもご注意ください。

### 旧バージョンのRuby on Rails

以前のバージョンのRuby on Railsに修正パッチを当てたい場合は、設定を行ってローカルのトラッキングブランチに切り替える必要があります。たとえば4-0-stableブランチに切り替える場合は以下のようにします。

```bash
$ git branch --track 4-0-stable rails/4-0-stable
$ git checkout 4-0-stable
```

TIP: [シェルのプロンプトにGitブランチ名を表示](http://qugstart.com/blog/git-and-svn/add-colored-git-branch-name-to-your-shell-prompt/)すると、今どのバージョンで作業しているかがその場で確認できるので便利です。

#### バックポート

変更がmasterにマージされると、その変更はRailsの次期メジャーリリースに採用されます。常にというわけではありませんが、変更を過去の安定版のメンテナンス用にバックポートできるとよい場合があります。一般に、セキュリティ修正とバグ修正は、バックポートの候補になります。新機能や動作変更用パッチはバックポートの候補には採り入れられません。自分の変更がどちらに該当するかわからない場合は、余分な作業をせずに済むためにも、変更をバックポートする前にRailsチームのメンバーにご相談ください。

単純な修正をバックポートする最も簡単な方法は、[masterと自分の変更のdiffをとって対象ブランチに適用する](http://ariejan.net/2009/10/26/how-to-create-and-apply-a-patch-with-git)ことです。

最初に、masterと自分の変更のdiff以外に差分がないことを確認します。

```bash
$ git log master..HEAD
```

次にdiffを展開します。

```bash
$ git format-patch master --stdout > ~/my_changes.patch
```

対象ブランチに切り替えて変更を適用します。

```bash
$ git checkout -b my_backport_branch 4-2-stable
$ git apply ~/my_changes.patch
```

単純な変更であればこれで十分バックポートできます。しかし、複雑な変更を行っていた場合や、masterと対象ブランチの差が甚だしくなっている場合は、もう少し手を加える必要があるかもしれません。バックポートがどのぐらい難しくなるかは場合によって大きく異なります。ときには、それほどの手間をかけてバックポートするほどの意味がないこともあります。

コンフリクトをすべて解消してすべてのテストがパスすることを確認できたら、変更をプッシュして、バックポート用のプルリクエストを別に作成します。なお、古いブランチではビルドのターゲットがmasterと異なるセットになっている場合がありますのでご注意ください。できれば、対象となるブランチの`rails.gemspec`で許されているRubyバージョンのうち、最も古いRubyを用いてバックポートをローカルでテストしてからプルリクエストを送信するようにしてください。

以上で解説はおしまいです。ここから先は、どんな貢献をしようか楽しみつつ考えるとしましょう。

Railsコントリビュータ
------------------

貢献が認められた方々は[Railsコントリビュータ](http://contributors.rubyonrails.org)にその名を連ねています。
