# deploy_sample

Public repository

Flutter sample app CI/CD automation using github action

- use fastlane to keep certification and provisioning profile for ios build

## Fastlane

```
# 설치
$ gem install fastlane

# insert git repo to keep certification
$ fastlane match init

$ cat << EOF > ios/fastlane/Fastfile
platform :ios do
  desc "Build and sign the iOS app"
  lane :build_and_sign do
    match(type: "development") # 개발용 서명
    build_app(workspace: "Runner.xcworkspace", scheme: "Runner") # 앱 빌드
  end
end
EOF
```

### 주의사항

- MATCH_PASSWORD: 해당 repo에 대한 access password로 passphrase라고 표시됨 (이부분은 여러 개발자에게 공유되어야 하는 부분)
- APP_SPECIFIC_PASSWORD: app을 관리하는 apple developer portal을 2FA를 bypass하기 위해서 생성하는 일회용 password로 개발자들은 자신의 계정을 이용하여 만든다.
