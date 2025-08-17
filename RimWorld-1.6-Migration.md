
이 문서는 RimWorld 1.6 및 예정된 Odyssey DLC에서의 Humanoid Alien Races에 대한 바닐라 림월드 변경점과 호환성 업데이트 가이드입니다.  
현재 작성 중이며, 새로운 정보가 나오는 대로 업데이트될 예정입니다. 최신 정보를 원한다면 **[Alien Races Discord](http://discord.gg/XMCRj46)**에 참여하세요!

이 문서는 주로 Humanoid Alien Races에 특화된 게임 변경점에 초점을 두고 있습니다. 더 광범위한 게임 변경 기록과 공식 변경 로그, 모더용 가이드는 RimWorld 위키의 [RimWorld 1.6 모드 업데이트](https://rimworldwiki.com/wiki/Modding_Tutorials/RimWorld_1.6_Mod_Updates) 페이지를 참고하세요.

Humanoid Alien Races의 현재 개발 버전은 GitHub의 Dev 브랜치에서 다운로드하거나, 스팀 워크샵 항목 **[Humanoid Alien Races - Dev](https://steamcommunity.com/sharedfiles/filedetails/?id=2640710953)** 를 통해 받을 수 있습니다.  
단, 이는 라이브 버전과 다른 packageId를 가지므로 일부 모드에서 종속성 누락 오류를 표시할 수 있습니다. 이는 정상이며 무시해도 안전합니다. 단, 두 버전을 동시에 로드하면 게임이 깨집니다.

# RimWorld 1.6 핵심 변경점

일반적으로 RimWorld v1.6은 Humanoid Alien Races에 큰 영향을 주지 않은 것으로 보입니다. 만약 추가적인 변경이 필요하다면 Discord에서 알려주시면 이 문서를 업데이트하겠습니다.

* `<forceGender>`가 이제 RaceProperties의 필드로 추가되었습니다. 이는 해당 종족이 오직 한 성별로만 생성되도록 강제할 수 있으며, 이전처럼 모든 PawnKindDefs에 `<fixedGender>`를 지정할 필요가 없습니다.
* ScenarioDefs에 새로운 필드가 추가되어 어느 행성 레이어에서 시작하는지를 정의할 수 있습니다. 이를 누락하면 시나리오가 정상적으로 로드되지 않습니다. 커스텀 시나리오를 사용한다면 새로운 추상 클래스 `ScenarioBase`를 상속하는 것을 고려하세요.

# Odyssey DLC 호환성

작성 시점(2025-06-17) 기준으로, 아래 내용은 데이터마이닝을 통해 얻은 것이며 최종 DLC의 실제 내용과 다를 수 있습니다.

## StatDefs

모든 DLC 전용 StatDefs와 마찬가지로, Odyssey를 종속성으로 요구하지 않고 이를 사용할 경우 반드시 `MayRequire="Ludeon.RimWorld.Odyssey"`를 지정해야 합니다.

* VacuumResistance - 폰이 진공 환경(우주나 무산소 환경 등)에서 진공 화상 피해를 받는지를 결정하는 것으로 보입니다. 기본값은 0이며 1.0일 경우 완전 면역이 됩니다. 주목할 점은 정찰병 및 해병 갑옷 등 일부 바닐라 방어구가 VacuumResistance 업그레이드를 받아도 완전 면역은 아니므로, 폰은 진공 상태에서 무기한 생존할 수 없습니다.
* PilotingAbility
* FishingSpeed
* FishingYield
* GravshipRange - 아마도 Pawn 스탯이 아님
* SubstructureSupport - 아마도 Pawn 스탯이 아님

## FactionDefs

* 새로운 `<arrivalLayerWhitelist>` 항목이 추가되었으며, 이는 바닐라 기계류(Mechanoids) 진영에만 존재하는 것으로 보입니다. 여기에는 바닐라 `Surface` 레이어와 Odyssey의 `Orbit` 레이어가 MayRequire 조건으로 명시되어 있습니다. 이는 어떤 진영이 어떤 행성 레이어를 침공할 수 있는지를 제한하는 역할을 하는 것으로 보입니다.
