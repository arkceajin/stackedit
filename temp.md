### ElectricCarClusterビルドエラーの件

#### エラー発生の原因：
QtプロジェクトのElectricCarCluster.proファイルに記載されたソースのファイル名と実際のファイル名に頭文字のケースが不一致でした。大・小文字を区別するOSで開く場合、ファイル識別できないエラーが発生します。

#### テスト時にエラーが発見できなかった原因：
こちらの作業PCは古いバージョンWindowsです。デフォルトは大・小文字を区別しない設定でしたので、文字列のケースが不一致でも、プロジェクトのビルドができました。

#### 対策手順：
以下の手順でWindowsの大・小文字を区別しない設定を実施して、ElectricCarCluster(Fixなし版)がビルドできます。
1. WindowsのCMDまたPowerShellを管理者権限で起動します。
2. `fsutil.exe file setCaseSensitiveInfo C:\ElectricCarCluster disable`を入力して実行します。※`C:\ElectricCarCluster`はプロジェクトのフォルダーパスです。
3. QtCreatorでプロジェクトを開いてビルドします。
