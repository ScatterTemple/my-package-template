# Python プロジェクトテンプレート

このプロジェクトは、PEP 621 で宣言された Python の標準に従う Python プロジェクトを作成するためのテンプレートです。`pyproject.toml` ファイルを使用してプロジェクトを構成し、Flit を使用してビルドプロセスを簡素化し、PyPI に公開します。Flit は `setup.py` や `setup.cfg` ファイルを必要とせず、`pyproject.toml` ファイル内にプロジェクトのすべての設定を一元化します。このアプローチにより、開発の効率が向上し、プロジェクトメタデータ、依存関係、ビルド仕様を一箇所に集約することで、メンテナンス性を促進します。

## プロジェクト構成

- `.github/workflows`: ビルド、テスト、公開に使用される GitHub Actions を格納します。
- `.devcontainer/Dockerfile`: VSCode の開発コンテナ用 Dockerfile を格納します。Python 開発に必要な拡張機能がインストールされています。
- `.devcontainer/devcontainer.json`: VSCode 用開発コンテナの設定を格納します（使用する Docker イメージ、追加の拡張機能、プロジェクトディレクトリのマウント可否など）。
- `.vscode/settings.json`: プロジェクト固有の VSCode 設定（Python インタープリタ、コード自動整形の最大行長など）を格納します。
- `src`: 新しいソースコードを配置します。
- `tests`: ソースコードを検証するための Python テストケースを格納します。
- `pyproject.toml`: プロジェクトに関するメタデータや Python コードのフォーマット、静的解析、型チェック、ツール設定を記述します。

### `pyproject.toml`

`pyproject.toml` は、モダンな Python プロジェクトの一元的な設定ファイルです。このファイルにより、プロジェクトメタデータ、依存関係、開発ツールの設定を一箇所で管理し、一貫性とメンテナンス性を確保できます。このアプローチにより、プロジェクトのセットアップが簡素化され、高品質なコード作成に専念できるようになります。主な構成要素は次の通りです：

- プロジェクトメタデータ
- 必須およびオプションの依存関係
- 開発ツール設定（例: リンター、フォーマッター、テストランナー）
- ビルドシステム仕様

この特定の `pyproject.toml` ファイルでは、`[build-system]` セクションで Flit パッケージをビルドツールとして指定し、`[project]` セクションではプロジェクトの名前、説明、作成者、分類情報を提供します。`[project.optional-dependencies]` セクションでは pyspark などのオプション依存関係をリスト化し、`[project.urls]` セクションではドキュメント、ソースコード、問題追跡用の URL を提供します。

さらに、bandit、black、coverage、flake8、pyright、pytest、tox、pylint 用のさまざまな設定セクションが含まれています。これらのセクションでは、flake8 の最大行長や coverage の最小コードカバレッジ率などの各ツール設定を指定します。

#### ツールセクション

##### black

Black は、Python コードを PEP 8 スタイルガイドに準拠させるコードフォーマッターです。一貫性のあるコードスタイルを維持するために使用されます。

`pyproject.toml` ファイルでは最大行長や「高速」モードの使用可否が指定されます。Black は、プロジェクトディレクトリ内にある `pyproject.toml` 設定ファイルを使用して動作をカスタマイズすることが可能です。

##### coverage

Coverage は、テスト中に実行されたコード行と未実行のコード行をレポートするコードカバレッジ測定ツールです。

`pyproject.toml` ファイルでは分岐カバレッジの測定や、カバレッジが 100% を下回る場合にテストを失敗させる設定が含まれています。Coverage は pytest を含むさまざまなテストフレームワークと統合できます。

##### pytest

Pytest は、Python プロジェクト向けの多用途なテストフレームワークで、テストケースの作成と実行を簡素化します。Pytest スタイルおよび Unittest スタイルの両方に対応しており、柔軟なテストアプローチを提供します。主な機能には、クリーンなテスト環境を提供するフィクスチャ、コードの重複を減らすパラメータ化テスト、プラグインによる拡張性が含まれます。

`pyproject.toml` ファイルでは、integration、notebooks、gpu、spark、slow、unit などのテストマーカーが指定されています。また、テストカバレッジレポートの生成、Python パスの設定、xunit2 フォーマットでのテスト結果出力のオプションも含まれます。

##### pylint

Pylint は、コード内のエラーやスタイルの問題を特定する Python のリンターおよび静的解析ツールです。コードベースで見つかったエラー、警告、規約を詳細なレポートとして生成します。`pyproject.toml` ファイルでは、拡張機能の管理、警告抑制、出力形式、コードスタイル設定（最大関数引数やクラス属性など）が集中管理されています。

##### pyright

Pyright は、型アノテーションを使用してコードを解析し、型関連のエラーを検出する静的型チェッカーです。

`pyproject.toml` ファイルには、解析対象外のディレクトリ、仮想環境、欠損インポートや型スタブに関するレポート設定などの構成が含まれています。

##### flake8

Flake8 は、PEP 8 スタイルガイド違反や構文エラーをチェックするコードリンターです。

`pyproject.toml` ファイルには、最大行長、無視するエラー、スタイルガイドの指定などの設定が含まれています。

##### tox

Tox は、複数の環境やバージョンで Python パッケージのテストとビルドを自動化します。`pyproject.toml` ファイルの `[tool.tox]` セクションでは、4 つのテスト環境（py、integration、spark、all）が設定されています。

### 開発

#### Codespaces

GitHub Codespaces を使用して開発を簡素化し、コラボレーションを強化します。ブラウザやローカル VSCode から一貫したクラウドベースの開発環境にアクセスできます。

#### Devcontainer

VSCode の Dev Containers を使用して、Docker コンテナを完全な開発環境として使用します。`.devcontainer/devcontainer.json` により、カスタム開発環境を指定可能です。

#### セットアップ

`.devcontainer` および `.vscode` ディレクトリ内の 3 つのファイルで、必要な拡張機能とツールを備えた環境をセットアップできます。
