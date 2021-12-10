# UnityでOculusのゲーム開発メモ
## OculusIntegrationパッケージ準備
Unity Asset Storeからダウンロード  
https://assetstore.unity.com/packages/tools/integration/oculus-integration-82022

My Assetsに追加した後、Unityで`Window > Package Manager`に行って、左上の`Packages: `のドロップダウンを`Packages: My Assets`にして、Oculus Integrationをインポートする。

## ヘッドセット起動させるの設定
Unityのメニューから`edit > Project Settings > XR Plug-in Management`に行って、`Install XR Plug-in Management`ボタンを押す。  
XR Plug-in Managementメニューが見えたらOculusのところにチェックを付けるで完成。

## CameraRigを追加
Project Viewで`Assets > Oculus > VR > Prefabs`からOVRCameraRigのPrefabを引っ張ってHierarchy Viewに置く。

## コントローラー対応追加
`Assets > Oculus > VR > Prefabs`に行って、
OVRPlayerControllerをシーンに追加して、それからOVRControllerPrefabの中に使いたいコントローラーのPrefabを取って(Projectビューに置く)、シーンにあるOVRPlayerControllerの中に左と右コントローラーのPrefabを`OVRCameraRig > LeftHandAnchor > LeftControllerAnchor`と`OVRCameraRig > RightHandAchor > RightControllerAnchor`に追加する。

## C#でのコントローラーの操作
コントローラーの位置を取得
```cs
// Vector3
OVRInput.GetLocalControllerPosition(OVRInput.Controller.RTouch)
// Quarternion
OVRInput.GetLocalControllerRotation(OVRInput.Controller.RTouch)
```

コントローラーの操作の例
```cs
//A ボタンを押すと何かする
if(OVRInput.GetDown(OVRInput.RawButton.A)) {
    //何かする
}
```

## 注意点
プレイヤーの下にPlaneがないとプレイヤーが落下してしまう可能性がある。プレイヤーが落下したらコントローラー・手はぐちゃぐちゃになる。

#### 参考

コントローラー操作
https://framesynthesis.jp/tech/unity/touch/

弾を打つ
https://answers.unity.com/questions/1105218/how-to-make-an-object-shoot-a-projectile.html