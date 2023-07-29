## 認可の方法2つ
<div style="font-size: 0.8em;">
    <p>
        アイデンティティベース：IAMを利用して認可を行う<br>
        リソースベース：リソース自体に認可の情報を指定する
    </p>
</div>

<div style="display: flex; justify-content: space-around;margin-top: -20px;">
  <img src="img/iam-16.jpg" style="width: 70%;">
</div>

----
### 認可の分類
<div class="two-column">
    <div class="column">
        <ul>
            <li>アイデンティティベース
                <ul>
                    <li>AssumeRole
                        <ul>
                            <li>同一AWSアカウント
                                <ul>
                                    <li>AWSリソース</li>
                                    <li>IAM Role</li>
                                </ul>
                            </li>
                            <li>別AWSアカウント
                                <ul>
                                    <li>IAM Role</li>
                                </ul>
                            </li>
                        </ul>
                    </li>
                    <li>Cognito
                        <ul>
                            <li>認証者がAWS以外</li>
                            <li>認証者がAWS</li>
                        </ul>
                    </li>
                </ul>
            </li>
        </ul>
    </div>
    <div class="column">
        <ul>
            <li>リソースベース
                <ul>
                    <li>同一AWSアカウント</li>
                    <li>別AWSアカウント</li>
                </ul>
            </li>
        </ul>
    </div>
</div>

<style>
.two-column {
    display: flex;
    justify-content: space-around;
    align-items: flex-start;
    width: 100%;
    font-size: 0.8em;>

}
.column {
    flex-basis: 0;
    flex-grow: 1;
    max-width: 100%;
}
</style>


---
## AWSの認可の基本
<div style="font-size: 0.8em;">
    <p>
        principal：誰がこの認可を求めに来るか<br>
        resource：どのリソースへのアクションを許可するか<br>
        action：リソースに対する操作
    </p>
</div>

<div style="display: flex; justify-content: space-around;margin-top: -20px;">
  <img src="img/iam-17.jpg" style="width: 70%;">
</div>

----
### IAMの基本
<div style="font-size: 0.8em;">
    <p>
        信頼ポリシー：IAM-policyをリクエストするprincipalを指定<br>
        アクションポリシー：ResourceとActionを指定
    </p>
</div>

<div style="display: flex; justify-content: space-around;margin-top: -20px;">
  <img src="img/iam-18.jpg" style="width: 70%;">
</div>



----
### STSとassume role 1
<div style="font-size: 0.8em;">
    <p>
        STS：IAM-Roleを一時的に付与する機能<br>
        Assume role：指定したIAM-Roleを引き受ける機能
    </p>
</div>

<div style="display: flex; justify-content: space-around;margin-top: -20px;">
  <img src="img/iam-19.jpg" style="width: 70%;">
</div>

----
### STSとassume role 2
<div style="font-size: 0.8em;">
    <p>
        STS：IAM-Roleを一時的に付与する機能<br>
        Assume role：指定したIAM-Roleを引き受ける機能
    </p>
</div>

<div style="display: flex; justify-content: space-around;margin-top: -20px;">
  <img src="img/iam-20.jpg" style="width: 70%;">
</div>

----
### STSとassume role 3
<div style="font-size: 0.8em;">
    <p>
        STS：IAM-Roleを一時的に付与する機能<br>
        Assume role：指定したIAM-Roleを引き受ける機能
    </p>
</div>

<div style="display: flex; justify-content: space-around;margin-top: -20px;">
  <img src="img/iam-21.jpg" style="width: 70%;">
</div>










---
## アイデンティティーベース（AssumeRole)
<div style="font-size: 0.8em;">
    <p>
        以下の3パターンが挙げられる<br>
        同一AWSアカウント内部からAWSリソースがAssumeする場合<br>
        同一AWSアカウント内部からIAMRoleがAssumeする場合<br>
        別AWSアカウントからIAMRoleがAssumeする場合
    </p>
</div>

----
### 同一AWSアカウント内部からAWSリソースがAssumeする場合
<div style="font-size: 0.6em;">
    <p>
        AWSリソースは同一アカウント内のRoleのみassume可能<br>
        リソース側は特に設定が不要<br>
        Role側の信頼ポリシーで対象リソースを認めておく
    </p>
</div>

<div style="display: flex; justify-content: space-around;margin-top: -20px;">
  <img src="img/iam-22.jpg" style="width: 70%;">
</div>



----
### 同一AWSアカウント内部からIAMRoleがAssumeする場合
<div style="font-size: 0.8em;">
    <p>
        assumeするRole-BのアクションポリシーでRole-Aをstsする内容を書いておく
    </p>
</div>

<div style="display: flex; justify-content: space-around;margin-top: -20px;">
  <img src="img/iam-23.jpg" style="width: 70%;">
</div>


----
### 別AWSアカウントからIAMRoleがAssumeする場合
<div style="font-size: 0.8em;">
    <p>
        assumeするRole-XのアクションポリシーでRole-Aをstsする内容を書いておく    
    </p>
</div>

<div style="display: flex; justify-content: space-around;margin-top: -20px;">
  <img src="img/iam-24.jpg" style="width: 70%;">
</div>








---
## アイデンティティーベース（Cognito)
<div style="font-size: 0.8em;">
    <p>
        以下の2パターンについて説明する<br>
        認証相手が別AWSアカウント以外場合<br>
        認証相手が別AWSアカウントの場合
    </p>
</div>

----
### 認証相手が別AWSアカウント以外場合
<div style="font-size: 0.8em;">
    <p>
        CognitoにID/PWで認証してクレデンシャルを払い出す
    </p>
</div>

<div style="display: flex; justify-content: space-around;margin-top: -20px;">
  <img src="img/iam-25.jpg" style="width: 70%;">
</div>

----
### 認証相手が別AWSアカウントの場合
<div style="font-size: 0.8em;">
    <p>
        CognitoにID/PWで認証してクレデンシャルを払い出す
    </p>
</div>
<div style="display: flex; justify-content: space-around;margin-top: -20px;">
  <img src="img/iam-26.jpg" style="width: 70%;">
</div>






---

## アイデンティティベースによる別AWSアカウントと連携する際の注意
----
### 古いロールを一時的に捨てる
<div style="font-size: 0.8em;">
    <p>
        Roleを持っている人がassumeかcognitoで別Roleを受け取る<br>
        元々持っていたRoleを一時的に捨てる（帽子の履き替え）
    </p>
</div>

[IAMロールの切り替え](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/id_roles_use_switch-role-cli.html)

<div style="display: flex; justify-content: space-around;margin-top: -20px;">
  <img src="img/iam-27.jpg" style="width: 70%;">
</div>

----
### 古いロールを捨てると古いロールに紐づいた認可を捨てる
<div style="font-size: 0.7em;">
    <p>
        古いロールを一時的に捨てるということは、元々アクセスできていたリソースにアクセスできなくなるということ<br>
        以下の例だと青い帽子になると、左側のS3にはアクセスできなくなる
    </p>
</div>

<div style="display: flex; justify-content: space-around;margin-top: -20px;">
  <img src="img/iam-28.jpg" style="width: 70%;">
</div>










---
## リソースベース
<div style="font-size: 0.8em;">
    <p>
        以下の2パターンについて説明する<br>
        同一AWSアカウント内部からアクセスする場合<br>
        別AWSアカウントからアクセスする場合
    </p>
</div>

----
### 同一AWSアカウント内部からアクセス
<div style="font-size: 0.8em;">
    <p>
        Resource側にprincipal、Resource、Action全てを書くだけでアクセス可能
    </p>
</div>

<div style="display: flex; justify-content: space-around;margin-top: -20px;">
  <img src="img/iam-29.jpg" style="width: 70%;">
</div>

----
### 別AWSアカウントからアクセス
<div style="font-size: 0.65em;">
    <p>
        Resouce側にprincipal、Resouce、Action全てを書いておく<br>
        加えて、アクセスするRoleにResouceとActionを書いておくとアクセス可能<br>
        ポイントはRoleにポリシーが付与された形になるので帽子の履き替えが不要
    </p>
</div>

<div style="display: flex; justify-content: space-around;margin-top: -20px;">
  <img src="img/iam-30.jpg" style="width: 70%;">
</div>
