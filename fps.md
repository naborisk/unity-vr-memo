# UnityでVR FPSゲームを作りましょう！
## 射撃の実装
VRの基本の操作が実装できたら弾の実装をしましょう。  
まず、弾のprefabが必要です。prefabとは単にいうとテンプレートみたいなものです。  
弾のprefabは簡単なキューブかスフィアでもいいので、今回はスフィアで作ります。  
![スフィア作成](img/sphere-create.png =x200)

これでスフィアが作成されたが、まだprefabではないです。  
prefabにする方法はHierarchyビューからスフィアを引っ張ってProjectビューに置くと完成です。  
![スフィアプレファブ](img/sphere-prefab.png =x200)

prefabを作成できたらHierarchyビューからスフィアを消してもいいです。

次はさっき作成したprefabを名前を"Bullet"と付けて、以下のコードをシーン内のGameObjectのスクリプトに書く。今回はGameControllerといういろいろなものを処理するオブジェクトを作成して使います。
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class GameController : MonoBehaviour {
    public GameObject projectile;

    void Update() {

    }
}
```
以上のように`public GameObject projectile;`を作って、ProjectビューからInspectorビューにあるGameControllerのスクリプトのProjectile欄にBulletを引っ張って置くとコードでこのprefabを使えます。

![弾をコードに追加](img/add-projectile =x200)

弾を撃つため、コードの`Update()`内でキーの判定を書いて、以下のように実装する。
```cs
void Update() {
    //テストのため今はキーボードのSpaceキーを使う
    if(Input.GetKeyDown(KeyCode.Space)) {
        GameObject bullet = Instantiate(projectile, transform.position, transform.rotation) as GameObject;
        bullet.GetComponent<Rigidbody>().AddForce(transform.forward * 500);
    }
}
```
以上のコードでテストのためまだVRのコントローラー使用しないが、キーボードのSpaceキーを使います。  
以上のように実装すればゲーム内でSpaceキーを押すとGameControllerの位置から弾が出るはずです。