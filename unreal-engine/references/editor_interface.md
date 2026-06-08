# Unreal-Engine - Editor Interface

**Pages:** 1191

---

## AbilitySystemGameFeatureActions

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AbilitySystemGameFeatureActions

**Contents:**
- AbilitySystemGameFeatureActions
- Navigation
- Classes



---

## ACLPluginEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ACLPluginEditor

**Contents:**
- ACLPluginEditor
- Navigation
- Classes
- Interfaces



---

## ACLPlugin

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ACLPlugin

**Contents:**
- ACLPlugin
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

FQuat4f RTM_SIMD_CALL ACLQuatToUE ( rtm::quatf_arg0 Input )

FTransform RTM_SIMD_CALL ACLTransformToUE ( rtm::qvvf_arg0 Input )

FVector3f RTM_SIMD_CALL ACLVector3ToUE ( rtm::vector4f_arg0 Input )

acl::track_array_qvvf BuildACLTransformTrackArray ( ACLAllocator& AllocatorImpl, const FCompressibleAnimData& CompressibleAnimData, float DefaultVirtualVertexDistance, float SafeVirtualVertexDistance, bool bBuildAdditiveBase, ACLPhantomTrackMode PhantomTrackMode )

acl::compression_level8 GetCompressionLevel ( ACLCompressionLevel Level )

uint32 GetNumSamples ( const FCompressibleAnimData& CompressibleAnimData )

acl::rotation_format8 GetRotationFormat ( ACLRotationFormat Format )

float GetSequenceLength ( const UAnimSequence& AnimSeq )

acl::vector_format8 GetVectorFormat ( ACLVectorFormat Format )

FQuat RTM_SIMD_CALL UEQuatCast ( const FQuat4f& Input )

rtm::quatf RTM_SIMD_CALL UEQuatToACL ( const FQuat4f& Input )

rtm::quatf RTM_SIMD_CALL UEQuatToACL ( const FQuat& Input )

FVector RTM_SIMD_CALL UEVector3Cast ( const FVector3f& Input )

FVector RTM_SIMD_CALL UEVector3Cast ( const FVector3d& Input )

rtm::vector4f RTM_SIMD_CALL UEVector3ToACL ( const FVector3f& Input )

rtm::vector4f RTM_SIMD_CALL UEVector3ToACL ( const FVector& Input )



---

## ActorLayerUtilities

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ActorLayerUtilities

**Contents:**
- ActorLayerUtilities
- Navigation
- Classes
- Structs



---

## ActorModifierCoreBlueprint

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ActorModifierCoreBlueprint

**Contents:**
- ActorModifierCoreBlueprint
- Navigation
- Classes



---

## ActorModifierCoreEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ActorModifierCoreEditor

**Contents:**
- ActorModifierCoreEditor
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## ActorModifierCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ActorModifierCore

**Contents:**
- ActorModifierCore
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

UActorModifierCoreBase * UE::ActorModifierCore::Utilities::FindFirstActorModifierByClass ( const AActor* InStartActor, const TSubclassOf< UActorModifierCoreBase >& InModifierClass )



---

## ActorModifierEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ActorModifierEditor

**Contents:**
- ActorModifierEditor
- Navigation
- Classes



---

## ActorModifierLayout

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ActorModifierLayout

**Contents:**
- ActorModifierLayout
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## ActorModifierRendering

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ActorModifierRendering

**Contents:**
- ActorModifierRendering
- Navigation
- Classes



---

## ActorModifier

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ActorModifier

**Contents:**
- ActorModifier
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

ENUM_CLASS_FLAGS ( EActorModifierAxis )

bool operator! ( EActorModifierVisibilityActor E )

EActorModifierVisibilityActor operator& ( EActorModifierVisibilityActor Lhs, EActorModifierVisibilityActor Rhs )

EActorModifierVisibilityActor & operator&= ( EActorModifierVisibilityActor& Lhs, EActorModifierVisibilityActor Rhs )

EActorModifierVisibilityActor operator^ ( EActorModifierVisibilityActor Lhs, EActorModifierVisibilityActor Rhs )

EActorModifierVisibilityActor & operator^= ( EActorModifierVisibilityActor& Lhs, EActorModifierVisibilityActor Rhs )

EActorModifierVisibilityActor operator| ( EActorModifierVisibilityActor Lhs, EActorModifierVisibilityActor Rhs )

EActorModifierVisibilityActor & operator|= ( EActorModifierVisibilityActor& Lhs, EActorModifierVisibilityActor Rhs )

EActorModifierVisibilityActor operator~ ( EActorModifierVisibilityActor E )

FRotator UE::ActorModifier::ActorUtils::FindLookAtRotation ( const FVector& InEyePosition, const FVector& InTargetPosition, EActorModifierAxis InAxis, bool bInFlipAxis )

FBox UE::ActorModifier::ActorUtils::GetActorBounds ( const AActor* InActor )

FBox UE::ActorModifier::ActorUtils::GetActorsBounds ( const TSet< TWeakObjectPtr< AActor > >& InActors, const FTransform& InReferenceTransform, bool bInSkipHidden )

FBox UE::ActorModifier::ActorUtils::GetActorsBounds ( AActor* InActor, bool bInIncludeChildren, bool bInSkipHidden )

FBox UE::ActorModifier::ActorUtils::GetActorsBounds ( const TSet< TWeakObjectPtr< AActor > >& InActors, const FTransform& InReferenceTransform, bool bInSkipHidden, bool bInTransformBox )

FOrientedBox UE::ActorModifier::ActorUtils::GetOrientedBox ( const FBox& InLocalBox, const FTransform& InWorldTransform )

FVector UE::ActorModifier::ActorUtils::GetVectorAxis ( int32 InAxis )

bool UE::ActorModifier::ActorUtils::IsActorVisible ( const AActor* InActor )

bool UE::ActorModifier::ActorUtils::IsAxisVectorEquals ( const FVector& InVectorA, const FVector& InVectorB, int32 InCompareAxis )



---

## ActorPalette

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ActorPalette

**Contents:**
- ActorPalette
- Navigation
- Classes



---

## ActorSequence

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ActorSequence

**Contents:**
- ActorSequence
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## AdjustEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AdjustEditor

**Contents:**
- AdjustEditor
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## ADOSupport

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ADOSupport

**Contents:**
- ADOSupport
- Navigation
- Interfaces



---

## AdvancedRenamer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AdvancedRenamer

**Contents:**
- AdvancedRenamer
- Navigation
- Interfaces



---

## AESGCMHandlerComponent

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AESGCMHandlerComponent

**Contents:**
- AESGCMHandlerComponent
- Navigation
- Classes
- Enums
  - Public
- Functions
  - Public

DECLARE_NETRESULT_ENUM ( EAESGCMNetResult )

const TCHAR * LexToString ( EAESGCMNetResult Enum )



---

## AESHandlerComponent

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AESHandlerComponent

**Contents:**
- AESHandlerComponent
- Navigation
- Classes



---

## AISupportModule

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AISupportModule

**Contents:**
- AISupportModule
- Navigation
- Interfaces



---

## AjaCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AjaCore

**Contents:**
- AjaCore
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public



---

## AjaMediaOutput

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AjaMediaOutput

**Contents:**
- AjaMediaOutput
- Navigation
- Classes
- Interfaces
- Enums
  - Public



---

## AjaMedia

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AjaMedia

**Contents:**
- AjaMedia
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## AlembicImporter

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AlembicImporter

**Contents:**
- AlembicImporter
- Navigation
- Classes
- Interfaces



---

## AlembicLibrary

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AlembicLibrary

**Contents:**
- AlembicLibrary
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Constants
- Functions
  - Public

bool operator! ( EFrameReadFlags E )

EFrameReadFlags operator& ( EFrameReadFlags Lhs, EFrameReadFlags Rhs )

EFrameReadFlags & operator&= ( EFrameReadFlags& Lhs, EFrameReadFlags Rhs )

EFrameReadFlags operator^ ( EFrameReadFlags Lhs, EFrameReadFlags Rhs )

EFrameReadFlags & operator^= ( EFrameReadFlags& Lhs, EFrameReadFlags Rhs )

EFrameReadFlags operator| ( EFrameReadFlags Lhs, EFrameReadFlags Rhs )

EFrameReadFlags & operator|= ( EFrameReadFlags& Lhs, EFrameReadFlags Rhs )

EFrameReadFlags operator~ ( EFrameReadFlags E )



---

## AMFCodecs

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AMFCodecs

**Contents:**
- AMFCodecs
- Navigation
- Classes
- Structs
- Functions
  - Public

DECLARE_TYPEID ( FVideoDecoderConfigAMF )

DECLARE_TYPEID ( FVideoEncoderConfigAMF )

DECLARE_TYPEID ( FAMF, AMFCODECS_API )

DECLARE_TYPEID ( amf::AMFSurfacePtr, AMFCODECS_API )



---

## AnalyticsBlueprintLibrary

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AnalyticsBlueprintLibrary

**Contents:**
- AnalyticsBlueprintLibrary
- Navigation
- Classes
- Structs



---

## AnalyticsMulticastEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AnalyticsMulticastEditor

**Contents:**
- AnalyticsMulticastEditor
- Navigation
- Classes



---

## AnalyticsMulticast

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AnalyticsMulticast

**Contents:**
- AnalyticsMulticast
- Navigation
- Classes



---

## AnimationBudgetAllocator

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AnimationBudgetAllocator

**Contents:**
- AnimationBudgetAllocator
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## AnimationLocomotionLibraryEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AnimationLocomotionLibraryEditor

**Contents:**
- AnimationLocomotionLibraryEditor
- Navigation
- Classes
- Interfaces
- Enums
  - Public



---

## AnimationLocomotionLibraryRuntime

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AnimationLocomotionLibraryRuntim-

**Contents:**
- AnimationLocomotionLibraryRuntime
- Navigation
- Classes



---

## AnimationModifierLibrary

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AnimationModifierLibrary

**Contents:**
- AnimationModifierLibrary
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

ENUM_CLASS_FLAGS ( EMotionExtractor_MotionType )

ENUM_RANGE_BY_VALUES ( EMotionExtractor_MotionType, EMotionExtractor_MotionType::Translation, EMotionExtractor_MotionType::Rotation, EMotionExtractor_MotionType::Scale, EMotionExtractor_MotionType::TranslationSpeed, EMotionExtractor_MotionType::RotationSpeed )

bool EnumHasAnyFlags ( int32 Flags, EMotionExtractor_MotionType Contains )



---

## AnimationSharingEd

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AnimationSharingEd

**Contents:**
- AnimationSharingEd
- Navigation
- Classes
- Functions
  - Static

static UEnum * GetStateEnumClass ( const TSharedPtr< IPropertyHandle >& InProperty )



---

## AnimationSharing

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AnimationSharing

**Contents:**
- AnimationSharing
- Navigation
- Classes
- Structs
- Typedefs
- Variables
  - Public



---

## AnimationWarpingEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AnimationWarpingEditor

**Contents:**
- AnimationWarpingEditor
- Navigation
- Classes
- Interfaces



---

## AnimationWarpingRuntime

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AnimationWarpingRuntime

**Contents:**
- AnimationWarpingRuntime
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## AnimatorKitSettings

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AnimatorKitSettings

**Contents:**
- AnimatorKitSettings
- Navigation
- Classes



---

## AnimToTextureEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AnimToTextureEditor

**Contents:**
- AnimToTextureEditor
- Navigation
- Classes
- Structs
- Typedefs
- Functions
  - Public

void AnimToTexture_Private::VectorToColor ( const V& Vector, C& Color )

bool AnimToTexture_Private::WriteSkinWeightsToTexture ( const TArray< VertexSkinWeightFour >& SkinWeights, const int32 NumBones, const int32 RowsPerFrame, const int32 Height, const int32 Width, UTexture2D* Texture )

bool AnimToTexture_Private::WriteToTexture ( UTexture2D* Texture, const uint32 Height, const uint32 Width, const TArray< typename TextureSettings::ColorType >& Data )

bool AnimToTexture_Private::WriteVectorsToTexture ( const TArray< V >& Vectors, const int32 NumFrames, const int32 RowsPerFrame, const int32 Height, const int32 Width, UTexture2D* Texture )



---

## AnimToTexture

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AnimToTexture

**Contents:**
- AnimToTexture
- Navigation
- Classes
- Structs
- Enums
  - Public
- Constants



---

## ApexDestruction

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ApexDestruction

**Contents:**
- ApexDestruction
- Navigation
- Classes
- Structs
- Enums
  - Public
- Variables
  - Public
- Functions
  - Public

FDestructibleAdvancedParameters()

FDestructibleChunkParameters()

FDestructibleDamageParameters()

FDestructibleDebrisParameters()

FDestructibleDepthParameters()

FDestructibleParametersFlag()

FDestructibleSpecialHierarchyDepths()

FUpdateChunksInfo ( int32 InChunkIndex, const FTransform& InWorldTM )

class UE_DEPRECATED (

class UE_DEPRECATED (



---

## ArchVisCharacter

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ArchVisCharacter

**Contents:**
- ArchVisCharacter
- Navigation
- Classes



---

## ARUtilities

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ARUtilities

**Contents:**
- ARUtilities
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## AssetManagerEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AssetManagerEditor

**Contents:**
- AssetManagerEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## AssetReferenceRestrictions

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AssetReferenceRestrictions

**Contents:**
- AssetReferenceRestrictions
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## AssetSearch

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AssetSearch

**Contents:**
- AssetSearch
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## AssetTags

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AssetTags

**Contents:**
- AssetTags
- Navigation
- Classes



---

## AsyncMessageSystem

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AsyncMessageSystem

**Contents:**
- AsyncMessageSystem
- Navigation
- Classes
- Structs
- Interfaces



---

## AudioCaptureEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioCaptureEditor

**Contents:**
- AudioCaptureEditor
- Navigation
- Structs
- Interfaces



---

## AudioCaptureTimecodeProvider

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioCaptureTimecodeProvider

**Contents:**
- AudioCaptureTimecodeProvider
- Navigation
- Classes



---

## AudioCapture

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioCapture

**Contents:**
- AudioCapture
- Navigation
- Classes
- Structs



---

## AudioExperimentalRuntime

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioExperimentalRuntime

**Contents:**
- AudioExperimentalRuntime
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public
  - Static

const TCHAR * LexToString ( const ESpeakerShortNames InSpeaker )

static uint32 Audio::SimpleAllocBasePrivate::GetDefaultSizeToAlignment ( const uint32 InSize )



---

## AudioGameplayTests

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioGameplayTests

**Contents:**
- AudioGameplayTests
- Navigation
- Classes



---

## AudioGameplayVolumeEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioGameplayVolumeEditor

**Contents:**
- AudioGameplayVolumeEditor
- Navigation
- Classes



---

## AudioGameplayVolume

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioGameplayVolume

**Contents:**
- AudioGameplayVolume
- Navigation
- Classes
- Structs



---

## AudioGameplay

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioGameplay

**Contents:**
- AudioGameplay
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

bool operator! ( AudioGameplay::EComponentPayload E )

AudioGameplay::EComponentPayload operator& ( AudioGameplay::EComponentPayload Lhs, AudioGameplay::EComponentPayload Rhs )

AudioGameplay::EComponentPayload & operator&= ( AudioGameplay::EComponentPayload& Lhs, AudioGameplay::EComponentPayload Rhs )

AudioGameplay::EComponentPayload operator^ ( AudioGameplay::EComponentPayload Lhs, AudioGameplay::EComponentPayload Rhs )

AudioGameplay::EComponentPayload & operator^= ( AudioGameplay::EComponentPayload& Lhs, AudioGameplay::EComponentPayload Rhs )

AudioGameplay::EComponentPayload operator| ( AudioGameplay::EComponentPayload Lhs, AudioGameplay::EComponentPayload Rhs )

AudioGameplay::EComponentPayload & operator|= ( AudioGameplay::EComponentPayload& Lhs, AudioGameplay::EComponentPayload Rhs )

AudioGameplay::EComponentPayload operator~ ( AudioGameplay::EComponentPayload E )



---

## AudioInsightsEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioInsightsEditor

**Contents:**
- AudioInsightsEditor
- Navigation
- Classes
- Interfaces



---

## AudioInsights

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioInsights

**Contents:**
- AudioInsights
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

bool UE::Audio::Insights::operator! ( ESoundDashboardFilterFlags E )

ESoundDashboardFilterFlags UE::Audio::Insights::operator& ( ESoundDashboardFilterFlags Lhs, ESoundDashboardFilterFlags Rhs )

ESoundDashboardFilterFlags & UE::Audio::Insights::operator&= ( ESoundDashboardFilterFlags& Lhs, ESoundDashboardFilterFlags Rhs )

ESoundDashboardFilterFlags UE::Audio::Insights::operator^ ( ESoundDashboardFilterFlags Lhs, ESoundDashboardFilterFlags Rhs )

ESoundDashboardFilterFlags & UE::Audio::Insights::operator^= ( ESoundDashboardFilterFlags& Lhs, ESoundDashboardFilterFlags Rhs )

ESoundDashboardFilterFlags UE::Audio::Insights::operator| ( ESoundDashboardFilterFlags Lhs, ESoundDashboardFilterFlags Rhs )

ESoundDashboardFilterFlags & UE::Audio::Insights::operator|= ( ESoundDashboardFilterFlags& Lhs, ESoundDashboardFilterFlags Rhs )

ESoundDashboardFilterFlags UE::Audio::Insights::operator~ ( ESoundDashboardFilterFlags E )



---

## AudioModulationEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioModulationEditor

**Contents:**
- AudioModulationEditor
- Navigation
- Classes



---

## AudioModulation

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioModulation

**Contents:**
- AudioModulation
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## AudioMotorSimDebug

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioMotorSimDebug

**Contents:**
- AudioMotorSimDebug
- Navigation
- Classes



---

## AudioMotorSimStandardComponents

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioMotorSimStandardComponents

**Contents:**
- AudioMotorSimStandardComponents
- Navigation
- Classes
- Structs



---

## AudioMotorSim

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioMotorSim

**Contents:**
- AudioMotorSim
- Navigation
- Classes
- Structs
- Interfaces
- Variables
  - Public
- Functions
  - Public

float AudioMotorSim::CmsToKmh ( const float InSpeed )

float AudioMotorSim::KmhToCms ( const float InSpeed )



---

## AudioSynesthesiaCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioSynesthesiaCore

**Contents:**
- AudioSynesthesiaCore
- Navigation
- Classes
- Structs
- Interfaces



---

## AudioSynesthesiaEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioSynesthesiaEditor

**Contents:**
- AudioSynesthesiaEditor
- Navigation
- Classes
- Interfaces
- Variables
  - Public



---

## AudioSynesthesia

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioSynesthesia

**Contents:**
- AudioSynesthesia
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public



---

## AudioWidgetsCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioWidgetsCore

**Contents:**
- AudioWidgetsCore
- Navigation
- Classes
- Structs
- Functions
  - Public

bool operator== ( const FAudioMeterChannelInfo& Lhs, const FAudioMeterChannelInfo& Rhs )



---

## AudioWidgetsEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioWidgetsEditor

**Contents:**
- AudioWidgetsEditor
- Navigation
- Classes



---

## AudioWidgets

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AudioWidgets

**Contents:**
- AudioWidgets
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

FCursorReply AudioWidgetsUtils::RouteCursorQuery ( const FPointerEvent& CursorEvent, TArrayView< const TSharedPtr< SWidget > > WidgetsStack, const bool bReverse )

FReply AudioWidgetsUtils::RouteMouseInput ( WidgetMouseInputFunction InputFunction, const FPointerEvent& MouseEvent, TArrayView< TSharedPtr< SWidget > > WidgetsStack, const bool bReverse )

void SampledSequenceDrawingUtils::GenerateEvenlySplitGridForGeometry ( TArray< FGridData >& OutGridData, const FGeometry& InAllottedGeometry, const uint16 NDimensions, const uint32 NumGridDivisions, const FSampledSequenceDrawingParams Params )

void SampledSequenceDrawingUtils::GenerateEvenlySplitGridForLine ( TArray< double >& OutDrawCoordinates, TArray< float >& OutLinePositionRatios, const float LineLength, const uint32 NumGridDivisions, bool bEmptyOutArrays )

void SampledSequenceDrawingUtils::GenerateMidpointSplitGridForGeometry ( TArray< FGridData >& OutGridData, const FGeometry& InAllottedGeometry, const uint16 NDimensions, const uint32 DivisionDepth, const FSampledSequenceDrawingParams Params )

void SampledSequenceDrawingUtils::GenerateMidpointSplitGridForLine ( TArray< double >& OutDrawCoordinates, TArray< float >& OutLinePositionRatios, const float LineLength, const uint32 DivisionDepth, bool bEmptyOutArrays )

void SampledSequenceDrawingUtils::GenerateSampleBinsCoordinatesForGeometry ( TArray< F2DLineCoordinates >& OutDrawCoordinates, const FGeometry& InAllottedGeometry, const TArray< TRange< float > >& InSampleBins, const uint16 NDimensions, const FSampledSequenceDrawingParams Params )

void SampledSequenceDrawingUtils::GenerateSequencedSamplesCoordinatesForGeometry ( TArray< FVector2D >& OutDrawCoordinates, TArrayView< const float > InSampleData, const FGeometry& InAllottedGeometry, const uint16 NDimensions, const FFixedSampledSequenceGridMetrics InGridMetrics, const FSampledSequenceDrawingParams Params )

void SampledSequenceDrawingUtils::GroupInterleavedSampledTSIntoMinMaxBins ( TArray< TRange< SamplesType > >& OutBins, const uint32 NumDesiredBins, const SamplesType* RawDataPtr, const uint32 TotalNumSamples, const uint32 SampleRate, const uint16 NDimensions, const float StartTime, float EndTime )

void SampledSequenceDrawingUtils::GroupInterleavedSamplesIntoMinMaxBins ( TArray< TRange< SamplesType > >& OutBins, const uint32 NumDesiredBins, const SamplesType* RawDataPtr, const uint32 TotalNumSamples, const uint16 NDimensions, const double StartRatio, double EndRatio )



---

## AutomatedPerfTesting

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AutomatedPerfTesting

**Contents:**
- AutomatedPerfTesting
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Static

static UWorld * AutomatedPerfTest::FindCurrentWorld()



---

## AutomationDriverTests

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AutomationDriverTests

**Contents:**
- AutomationDriverTests
- Navigation
- Classes



---

## AutomationUtilsEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AutomationUtilsEditor

**Contents:**
- AutomationUtilsEditor
- Navigation
- Classes



---

## AutomationUtils

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AutomationUtils

**Contents:**
- AutomationUtils
- Navigation
- Classes



---

## AvalancheAttributeEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheAttributeEditor

**Contents:**
- AvalancheAttributeEditor
- Navigation
- Interfaces



---

## AvalancheAttribute

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheAttribute

**Contents:**
- AvalancheAttribute
- Navigation
- Classes



---

## AvalancheCamera

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheCamera

**Contents:**
- AvalancheCamera
- Navigation
- Classes
- Structs



---

## AvalancheComponentVisualizers

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheComponentVisualizers

**Contents:**
- AvalancheComponentVisualizers
- Navigation
- Classes
- Structs
- Interfaces
- Variables
  - Public



---

## AvalancheCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheCore

**Contents:**
- AvalancheCore
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Variables
  - Public
- Functions
  - Public

TSharedPtr< InCastToType > UE::AvaCore::CastSharedPtr ( const TSharedPtr< IAvaTypeCastable >& InSharedPtr )

InPropertyType * UE::AvaCore::GetProperty ( FName InMemberPropertyName )



---

## AvalancheDataLink

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheDataLink

**Contents:**
- AvalancheDataLink
- Navigation
- Classes
- Structs



---

## AvalancheEditorCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheEditorCore

**Contents:**
- AvalancheEditorCore
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## AvalancheInteractiveToolsRuntime

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheInteractiveToolsRuntime

**Contents:**
- AvalancheInteractiveToolsRuntime
- Navigation
- Classes
- Interfaces



---

## AvalancheInteractiveTools

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheInteractiveTools

**Contents:**
- AvalancheInteractiveTools
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## AvalancheLevelViewport

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheLevelViewport

**Contents:**
- AvalancheLevelViewport
- Navigation
- Classes
- Structs



---

## AvalancheMaskEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheMaskEditor

**Contents:**
- AvalancheMaskEditor
- Navigation
- Functions
  - Static

static const FName UE::AvaMaskEditor::MotionDesignMaskEditorModeName ( "EditMode.MotionDesignMask" )



---

## AvalancheMask

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheMask

**Contents:**
- AvalancheMask
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

uint32 GetTypeHash ( const FAvaMask2DComponentMaterialPath& MaterialPath )



---

## AvalancheMediaEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheMediaEditor

**Contents:**
- AvalancheMediaEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## AvalancheMedia

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheMedia

**Contents:**
- AvalancheMedia
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

bool operator! ( EAvaBroadcastChange E )

bool operator! ( EAvaBroadcastChannelChange E )

bool operator! ( EAvaPlayableTransitionFlags E )

bool operator! ( EAvaPlayableTransitionEventFlags E )

bool operator! ( EAvaPlayableRCUpdateFlags E )

bool operator! ( EAvaRundownPageListChange E )

bool operator! ( EAvaRundownPageChanges E )

bool operator! ( EAvaPlayableEndPlayOptions E )

bool operator! ( EAvaPlayableRemoteControlChanges E )

bool operator! ( EAvaPlaybackStopOptions E )

bool operator! ( EAvaPlaybackUnloadOptions E )

bool operator! ( EAvaPlaybackPackageEventFlags E )

bool operator! ( EAvaRundownPageStopOptions E )

EAvaBroadcastChange operator& ( EAvaBroadcastChange Lhs, EAvaBroadcastChange Rhs )

EAvaBroadcastChannelChange operator& ( EAvaBroadcastChannelChange Lhs, EAvaBroadcastChannelChange Rhs )

EAvaPlayableTransitionFlags operator& ( EAvaPlayableTransitionFlags Lhs, EAvaPlayableTransitionFlags Rhs )

EAvaPlayableTransitionEventFlags operator& ( EAvaPlayableTransitionEventFlags Lhs, EAvaPlayableTransitionEventFlags Rhs )

EAvaPlayableRCUpdateFlags operator& ( EAvaPlayableRCUpdateFlags Lhs, EAvaPlayableRCUpdateFlags Rhs )

EAvaRundownPageListChange operator& ( EAvaRundownPageListChange Lhs, EAvaRundownPageListChange Rhs )

EAvaRundownPageChanges operator& ( EAvaRundownPageChanges Lhs, EAvaRundownPageChanges Rhs )

EAvaPlayableEndPlayOptions operator& ( EAvaPlayableEndPlayOptions Lhs, EAvaPlayableEndPlayOptions Rhs )

EAvaPlayableRemoteControlChanges operator& ( EAvaPlayableRemoteControlChanges Lhs, EAvaPlayableRemoteControlChanges Rhs )

EAvaPlaybackStopOptions operator& ( EAvaPlaybackStopOptions Lhs, EAvaPlaybackStopOptions Rhs )

EAvaPlaybackUnloadOptions operator& ( EAvaPlaybackUnloadOptions Lhs, EAvaPlaybackUnloadOptions Rhs )

EAvaPlaybackPackageEventFlags operator& ( EAvaPlaybackPackageEventFlags Lhs, EAvaPlaybackPackageEventFlags Rhs )

EAvaRundownPageStopOptions operator& ( EAvaRundownPageStopOptions Lhs, EAvaRundownPageStopOptions Rhs )

EAvaBroadcastChange & operator&= ( EAvaBroadcastChange& Lhs, EAvaBroadcastChange Rhs )

EAvaBroadcastChannelChange & operator&= ( EAvaBroadcastChannelChange& Lhs, EAvaBroadcastChannelChange Rhs )

EAvaPlayableTransitionFlags & operator&= ( EAvaPlayableTransitionFlags& Lhs, EAvaPlayableTransitionFlags Rhs )

EAvaPlayableTransitionEventFlags & operator&= ( EAvaPlayableTransitionEventFlags& Lhs, EAvaPlayableTransitionEventFlags Rhs )

EAvaPlayableRCUpdateFlags & operator&= ( EAvaPlayableRCUpdateFlags& Lhs, EAvaPlayableRCUpdateFlags Rhs )

EAvaRundownPageListChange & operator&= ( EAvaRundownPageListChange& Lhs, EAvaRundownPageListChange Rhs )

EAvaRundownPageChanges & operator&= ( EAvaRundownPageChanges& Lhs, EAvaRundownPageChanges Rhs )

EAvaPlayableEndPlayOptions & operator&= ( EAvaPlayableEndPlayOptions& Lhs, EAvaPlayableEndPlayOptions Rhs )

EAvaPlayableRemoteControlChanges & operator&= ( EAvaPlayableRemoteControlChanges& Lhs, EAvaPlayableRemoteControlChanges Rhs )

EAvaPlaybackStopOptions & operator&= ( EAvaPlaybackStopOptions& Lhs, EAvaPlaybackStopOptions Rhs )

EAvaPlaybackUnloadOptions & operator&= ( EAvaPlaybackUnloadOptions& Lhs, EAvaPlaybackUnloadOptions Rhs )

EAvaPlaybackPackageEventFlags & operator&= ( EAvaPlaybackPackageEventFlags& Lhs, EAvaPlaybackPackageEventFlags Rhs )

EAvaRundownPageStopOptions & operator&= ( EAvaRundownPageStopOptions& Lhs, EAvaRundownPageStopOptions Rhs )

EAvaBroadcastChange operator^ ( EAvaBroadcastChange Lhs, EAvaBroadcastChange Rhs )

EAvaBroadcastChannelChange operator^ ( EAvaBroadcastChannelChange Lhs, EAvaBroadcastChannelChange Rhs )

EAvaPlayableTransitionFlags operator^ ( EAvaPlayableTransitionFlags Lhs, EAvaPlayableTransitionFlags Rhs )

EAvaPlayableTransitionEventFlags operator^ ( EAvaPlayableTransitionEventFlags Lhs, EAvaPlayableTransitionEventFlags Rhs )

EAvaPlayableRCUpdateFlags operator^ ( EAvaPlayableRCUpdateFlags Lhs, EAvaPlayableRCUpdateFlags Rhs )

EAvaRundownPageListChange operator^ ( EAvaRundownPageListChange Lhs, EAvaRundownPageListChange Rhs )

EAvaRundownPageChanges operator^ ( EAvaRundownPageChanges Lhs, EAvaRundownPageChanges Rhs )

EAvaPlayableEndPlayOptions operator^ ( EAvaPlayableEndPlayOptions Lhs, EAvaPlayableEndPlayOptions Rhs )

EAvaPlayableRemoteControlChanges operator^ ( EAvaPlayableRemoteControlChanges Lhs, EAvaPlayableRemoteControlChanges Rhs )

EAvaPlaybackStopOptions operator^ ( EAvaPlaybackStopOptions Lhs, EAvaPlaybackStopOptions Rhs )

EAvaPlaybackUnloadOptions operator^ ( EAvaPlaybackUnloadOptions Lhs, EAvaPlaybackUnloadOptions Rhs )

EAvaPlaybackPackageEventFlags operator^ ( EAvaPlaybackPackageEventFlags Lhs, EAvaPlaybackPackageEventFlags Rhs )

EAvaRundownPageStopOptions operator^ ( EAvaRundownPageStopOptions Lhs, EAvaRundownPageStopOptions Rhs )

EAvaBroadcastChange & operator^= ( EAvaBroadcastChange& Lhs, EAvaBroadcastChange Rhs )

EAvaBroadcastChannelChange & operator^= ( EAvaBroadcastChannelChange& Lhs, EAvaBroadcastChannelChange Rhs )

EAvaPlayableTransitionFlags & operator^= ( EAvaPlayableTransitionFlags& Lhs, EAvaPlayableTransitionFlags Rhs )

EAvaPlayableTransitionEventFlags & operator^= ( EAvaPlayableTransitionEventFlags& Lhs, EAvaPlayableTransitionEventFlags Rhs )

EAvaPlayableRCUpdateFlags & operator^= ( EAvaPlayableRCUpdateFlags& Lhs, EAvaPlayableRCUpdateFlags Rhs )

EAvaRundownPageListChange & operator^= ( EAvaRundownPageListChange& Lhs, EAvaRundownPageListChange Rhs )

EAvaRundownPageChanges & operator^= ( EAvaRundownPageChanges& Lhs, EAvaRundownPageChanges Rhs )

EAvaPlayableEndPlayOptions & operator^= ( EAvaPlayableEndPlayOptions& Lhs, EAvaPlayableEndPlayOptions Rhs )

EAvaPlayableRemoteControlChanges & operator^= ( EAvaPlayableRemoteControlChanges& Lhs, EAvaPlayableRemoteControlChanges Rhs )

EAvaPlaybackStopOptions & operator^= ( EAvaPlaybackStopOptions& Lhs, EAvaPlaybackStopOptions Rhs )

EAvaPlaybackUnloadOptions & operator^= ( EAvaPlaybackUnloadOptions& Lhs, EAvaPlaybackUnloadOptions Rhs )

EAvaPlaybackPackageEventFlags & operator^= ( EAvaPlaybackPackageEventFlags& Lhs, EAvaPlaybackPackageEventFlags Rhs )

EAvaRundownPageStopOptions & operator^= ( EAvaRundownPageStopOptions& Lhs, EAvaRundownPageStopOptions Rhs )

EAvaBroadcastChange operator| ( EAvaBroadcastChange Lhs, EAvaBroadcastChange Rhs )

EAvaBroadcastChannelChange operator| ( EAvaBroadcastChannelChange Lhs, EAvaBroadcastChannelChange Rhs )

EAvaPlayableTransitionFlags operator| ( EAvaPlayableTransitionFlags Lhs, EAvaPlayableTransitionFlags Rhs )

EAvaPlayableTransitionEventFlags operator| ( EAvaPlayableTransitionEventFlags Lhs, EAvaPlayableTransitionEventFlags Rhs )

EAvaPlayableRCUpdateFlags operator| ( EAvaPlayableRCUpdateFlags Lhs, EAvaPlayableRCUpdateFlags Rhs )

EAvaRundownPageListChange operator| ( EAvaRundownPageListChange Lhs, EAvaRundownPageListChange Rhs )

EAvaRundownPageChanges operator| ( EAvaRundownPageChanges Lhs, EAvaRundownPageChanges Rhs )

EAvaPlayableEndPlayOptions operator| ( EAvaPlayableEndPlayOptions Lhs, EAvaPlayableEndPlayOptions Rhs )

EAvaPlayableRemoteControlChanges operator| ( EAvaPlayableRemoteControlChanges Lhs, EAvaPlayableRemoteControlChanges Rhs )

EAvaPlaybackStopOptions operator| ( EAvaPlaybackStopOptions Lhs, EAvaPlaybackStopOptions Rhs )

EAvaPlaybackUnloadOptions operator| ( EAvaPlaybackUnloadOptions Lhs, EAvaPlaybackUnloadOptions Rhs )

EAvaPlaybackPackageEventFlags operator| ( EAvaPlaybackPackageEventFlags Lhs, EAvaPlaybackPackageEventFlags Rhs )

EAvaRundownPageStopOptions operator| ( EAvaRundownPageStopOptions Lhs, EAvaRundownPageStopOptions Rhs )

EAvaBroadcastChange & operator|= ( EAvaBroadcastChange& Lhs, EAvaBroadcastChange Rhs )

EAvaBroadcastChannelChange & operator|= ( EAvaBroadcastChannelChange& Lhs, EAvaBroadcastChannelChange Rhs )

EAvaPlayableTransitionFlags & operator|= ( EAvaPlayableTransitionFlags& Lhs, EAvaPlayableTransitionFlags Rhs )

EAvaPlayableTransitionEventFlags & operator|= ( EAvaPlayableTransitionEventFlags& Lhs, EAvaPlayableTransitionEventFlags Rhs )

EAvaPlayableRCUpdateFlags & operator|= ( EAvaPlayableRCUpdateFlags& Lhs, EAvaPlayableRCUpdateFlags Rhs )

EAvaRundownPageListChange & operator|= ( EAvaRundownPageListChange& Lhs, EAvaRundownPageListChange Rhs )

EAvaRundownPageChanges & operator|= ( EAvaRundownPageChanges& Lhs, EAvaRundownPageChanges Rhs )

EAvaPlayableEndPlayOptions & operator|= ( EAvaPlayableEndPlayOptions& Lhs, EAvaPlayableEndPlayOptions Rhs )

EAvaPlayableRemoteControlChanges & operator|= ( EAvaPlayableRemoteControlChanges& Lhs, EAvaPlayableRemoteControlChanges Rhs )

EAvaPlaybackStopOptions & operator|= ( EAvaPlaybackStopOptions& Lhs, EAvaPlaybackStopOptions Rhs )

EAvaPlaybackUnloadOptions & operator|= ( EAvaPlaybackUnloadOptions& Lhs, EAvaPlaybackUnloadOptions Rhs )

EAvaPlaybackPackageEventFlags & operator|= ( EAvaPlaybackPackageEventFlags& Lhs, EAvaPlaybackPackageEventFlags Rhs )

EAvaRundownPageStopOptions & operator|= ( EAvaRundownPageStopOptions& Lhs, EAvaRundownPageStopOptions Rhs )

EAvaBroadcastChange operator~ ( EAvaBroadcastChange E )

EAvaBroadcastChannelChange operator~ ( EAvaBroadcastChannelChange E )

EAvaPlayableTransitionFlags operator~ ( EAvaPlayableTransitionFlags E )

EAvaPlayableTransitionEventFlags operator~ ( EAvaPlayableTransitionEventFlags E )

EAvaPlayableRCUpdateFlags operator~ ( EAvaPlayableRCUpdateFlags E )

EAvaRundownPageListChange operator~ ( EAvaRundownPageListChange E )

EAvaRundownPageChanges operator~ ( EAvaRundownPageChanges E )

EAvaPlayableEndPlayOptions operator~ ( EAvaPlayableEndPlayOptions E )

EAvaPlayableRemoteControlChanges operator~ ( EAvaPlayableRemoteControlChanges E )

EAvaPlaybackStopOptions operator~ ( EAvaPlaybackStopOptions E )

EAvaPlaybackUnloadOptions operator~ ( EAvaPlaybackUnloadOptions E )

EAvaPlaybackPackageEventFlags operator~ ( EAvaPlaybackPackageEventFlags E )

EAvaRundownPageStopOptions operator~ ( EAvaRundownPageStopOptions E )

bool UE::AvaRundown::IsPreviewPlayType ( EAvaRundownPagePlayType InPlayType )



---

## AvalancheModifiers

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheModifiers

**Contents:**
- AvalancheModifiers
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

bool operator! ( EAvaDynamicMeshConverterModifierType E )

EAvaDynamicMeshConverterModifierType operator& ( EAvaDynamicMeshConverterModifierType Lhs, EAvaDynamicMeshConverterModifierType Rhs )

EAvaDynamicMeshConverterModifierType & operator&= ( EAvaDynamicMeshConverterModifierType& Lhs, EAvaDynamicMeshConverterModifierType Rhs )

EAvaDynamicMeshConverterModifierType operator^ ( EAvaDynamicMeshConverterModifierType Lhs, EAvaDynamicMeshConverterModifierType Rhs )

EAvaDynamicMeshConverterModifierType & operator^= ( EAvaDynamicMeshConverterModifierType& Lhs, EAvaDynamicMeshConverterModifierType Rhs )

EAvaDynamicMeshConverterModifierType operator| ( EAvaDynamicMeshConverterModifierType Lhs, EAvaDynamicMeshConverterModifierType Rhs )

EAvaDynamicMeshConverterModifierType & operator|= ( EAvaDynamicMeshConverterModifierType& Lhs, EAvaDynamicMeshConverterModifierType Rhs )

EAvaDynamicMeshConverterModifierType operator~ ( EAvaDynamicMeshConverterModifierType E )



---

## AvalancheMRQ

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheMRQ

**Contents:**
- AvalancheMRQ
- Navigation
- Classes
- Structs



---

## AvalancheOutliner

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheOutliner

**Contents:**
- AvalancheOutliner
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

bool operator! ( EAvaOutlinerItemFlags E )

bool operator! ( EAvaOutlinerItemSelectionFlags E )

bool operator! ( EAvaOutlinerIgnoreNotifyFlags E )

bool operator! ( EAvaOutlinerItemViewMode E )

bool operator! ( EAvaOutlinerTypeFilterMode E )

bool operator! ( EAvaOutlinerAddItemFlags E )

EAvaOutlinerItemFlags operator& ( EAvaOutlinerItemFlags Lhs, EAvaOutlinerItemFlags Rhs )

EAvaOutlinerItemSelectionFlags operator& ( EAvaOutlinerItemSelectionFlags Lhs, EAvaOutlinerItemSelectionFlags Rhs )

EAvaOutlinerIgnoreNotifyFlags operator& ( EAvaOutlinerIgnoreNotifyFlags Lhs, EAvaOutlinerIgnoreNotifyFlags Rhs )

EAvaOutlinerItemViewMode operator& ( EAvaOutlinerItemViewMode Lhs, EAvaOutlinerItemViewMode Rhs )

EAvaOutlinerTypeFilterMode operator& ( EAvaOutlinerTypeFilterMode Lhs, EAvaOutlinerTypeFilterMode Rhs )

EAvaOutlinerAddItemFlags operator& ( EAvaOutlinerAddItemFlags Lhs, EAvaOutlinerAddItemFlags Rhs )

EAvaOutlinerItemFlags & operator&= ( EAvaOutlinerItemFlags& Lhs, EAvaOutlinerItemFlags Rhs )

EAvaOutlinerItemSelectionFlags & operator&= ( EAvaOutlinerItemSelectionFlags& Lhs, EAvaOutlinerItemSelectionFlags Rhs )

EAvaOutlinerIgnoreNotifyFlags & operator&= ( EAvaOutlinerIgnoreNotifyFlags& Lhs, EAvaOutlinerIgnoreNotifyFlags Rhs )

EAvaOutlinerItemViewMode & operator&= ( EAvaOutlinerItemViewMode& Lhs, EAvaOutlinerItemViewMode Rhs )

EAvaOutlinerTypeFilterMode & operator&= ( EAvaOutlinerTypeFilterMode& Lhs, EAvaOutlinerTypeFilterMode Rhs )

EAvaOutlinerAddItemFlags & operator&= ( EAvaOutlinerAddItemFlags& Lhs, EAvaOutlinerAddItemFlags Rhs )

EAvaOutlinerItemFlags operator^ ( EAvaOutlinerItemFlags Lhs, EAvaOutlinerItemFlags Rhs )

EAvaOutlinerItemSelectionFlags operator^ ( EAvaOutlinerItemSelectionFlags Lhs, EAvaOutlinerItemSelectionFlags Rhs )

EAvaOutlinerIgnoreNotifyFlags operator^ ( EAvaOutlinerIgnoreNotifyFlags Lhs, EAvaOutlinerIgnoreNotifyFlags Rhs )

EAvaOutlinerItemViewMode operator^ ( EAvaOutlinerItemViewMode Lhs, EAvaOutlinerItemViewMode Rhs )

EAvaOutlinerTypeFilterMode operator^ ( EAvaOutlinerTypeFilterMode Lhs, EAvaOutlinerTypeFilterMode Rhs )

EAvaOutlinerAddItemFlags operator^ ( EAvaOutlinerAddItemFlags Lhs, EAvaOutlinerAddItemFlags Rhs )

EAvaOutlinerItemFlags & operator^= ( EAvaOutlinerItemFlags& Lhs, EAvaOutlinerItemFlags Rhs )

EAvaOutlinerItemSelectionFlags & operator^= ( EAvaOutlinerItemSelectionFlags& Lhs, EAvaOutlinerItemSelectionFlags Rhs )

EAvaOutlinerIgnoreNotifyFlags & operator^= ( EAvaOutlinerIgnoreNotifyFlags& Lhs, EAvaOutlinerIgnoreNotifyFlags Rhs )

EAvaOutlinerItemViewMode & operator^= ( EAvaOutlinerItemViewMode& Lhs, EAvaOutlinerItemViewMode Rhs )

EAvaOutlinerTypeFilterMode & operator^= ( EAvaOutlinerTypeFilterMode& Lhs, EAvaOutlinerTypeFilterMode Rhs )

EAvaOutlinerAddItemFlags & operator^= ( EAvaOutlinerAddItemFlags& Lhs, EAvaOutlinerAddItemFlags Rhs )

EAvaOutlinerItemFlags operator| ( EAvaOutlinerItemFlags Lhs, EAvaOutlinerItemFlags Rhs )

EAvaOutlinerItemSelectionFlags operator| ( EAvaOutlinerItemSelectionFlags Lhs, EAvaOutlinerItemSelectionFlags Rhs )

EAvaOutlinerIgnoreNotifyFlags operator| ( EAvaOutlinerIgnoreNotifyFlags Lhs, EAvaOutlinerIgnoreNotifyFlags Rhs )

EAvaOutlinerItemViewMode operator| ( EAvaOutlinerItemViewMode Lhs, EAvaOutlinerItemViewMode Rhs )

EAvaOutlinerTypeFilterMode operator| ( EAvaOutlinerTypeFilterMode Lhs, EAvaOutlinerTypeFilterMode Rhs )

EAvaOutlinerAddItemFlags operator| ( EAvaOutlinerAddItemFlags Lhs, EAvaOutlinerAddItemFlags Rhs )

EAvaOutlinerItemFlags & operator|= ( EAvaOutlinerItemFlags& Lhs, EAvaOutlinerItemFlags Rhs )

EAvaOutlinerItemSelectionFlags & operator|= ( EAvaOutlinerItemSelectionFlags& Lhs, EAvaOutlinerItemSelectionFlags Rhs )

EAvaOutlinerIgnoreNotifyFlags & operator|= ( EAvaOutlinerIgnoreNotifyFlags& Lhs, EAvaOutlinerIgnoreNotifyFlags Rhs )

EAvaOutlinerItemViewMode & operator|= ( EAvaOutlinerItemViewMode& Lhs, EAvaOutlinerItemViewMode Rhs )

EAvaOutlinerTypeFilterMode & operator|= ( EAvaOutlinerTypeFilterMode& Lhs, EAvaOutlinerTypeFilterMode Rhs )

EAvaOutlinerAddItemFlags & operator|= ( EAvaOutlinerAddItemFlags& Lhs, EAvaOutlinerAddItemFlags Rhs )

EAvaOutlinerItemFlags operator~ ( EAvaOutlinerItemFlags E )

EAvaOutlinerItemSelectionFlags operator~ ( EAvaOutlinerItemSelectionFlags E )

EAvaOutlinerIgnoreNotifyFlags operator~ ( EAvaOutlinerIgnoreNotifyFlags E )

EAvaOutlinerItemViewMode operator~ ( EAvaOutlinerItemViewMode E )

EAvaOutlinerTypeFilterMode operator~ ( EAvaOutlinerTypeFilterMode E )

EAvaOutlinerAddItemFlags operator~ ( EAvaOutlinerAddItemFlags E )

bool UE::AvaOutliner::CompareOutlinerItemOrder ( const FAvaOutlinerItemPtr& A, const FAvaOutlinerItemPtr& B )

void UE::AvaOutliner::SplitItems ( const TArray< FAvaOutlinerItemPtr >& InItems, TArray< FAvaOutlinerItemPtr >& OutSortable, TArray< FAvaOutlinerItemPtr >& OutUnsortable )



---

## AvalancheRemoteControl

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheRemoteControl

**Contents:**
- AvalancheRemoteControl
- Navigation
- Classes
- Structs
- Interfaces



---

## AvalancheSceneRigEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheSceneRigEditor

**Contents:**
- AvalancheSceneRigEditor
- Navigation
- Classes
- Interfaces



---

## AvalancheSceneRig

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheSceneRig

**Contents:**
- AvalancheSceneRig
- Navigation
- Classes
- Variables
  - Public



---

## AvalancheSceneStateBlueprint

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheSceneStateBlueprint

**Contents:**
- AvalancheSceneStateBlueprint
- Navigation
- Classes



---

## AvalancheSceneState

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheSceneState

**Contents:**
- AvalancheSceneState
- Navigation
- Classes
- Structs



---

## AvalancheSceneTree

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheSceneTree

**Contents:**
- AvalancheSceneTree
- Navigation
- Structs
- Enums
  - Public



---

## AvalancheSequencer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheSequencer

**Contents:**
- AvalancheSequencer
- Navigation
- Classes
- Structs
- Interfaces



---

## AvalancheSequence

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheSequence

**Contents:**
- AvalancheSequence
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

bool operator! ( EAvaMarkRoleReply E )

EAvaMarkRoleReply operator& ( EAvaMarkRoleReply Lhs, EAvaMarkRoleReply Rhs )

EAvaMarkRoleReply & operator&= ( EAvaMarkRoleReply& Lhs, EAvaMarkRoleReply Rhs )

EAvaMarkRoleReply operator^ ( EAvaMarkRoleReply Lhs, EAvaMarkRoleReply Rhs )

EAvaMarkRoleReply & operator^= ( EAvaMarkRoleReply& Lhs, EAvaMarkRoleReply Rhs )

EAvaMarkRoleReply operator| ( EAvaMarkRoleReply Lhs, EAvaMarkRoleReply Rhs )

EAvaMarkRoleReply & operator|= ( EAvaMarkRoleReply& Lhs, EAvaMarkRoleReply Rhs )

EAvaMarkRoleReply operator~ ( EAvaMarkRoleReply E )



---

## AvalancheShapesEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheShapesEditor

**Contents:**
- AvalancheShapesEditor
- Navigation
- Variables
  - Public



---

## AvalancheShapes

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheShapes

**Contents:**
- AvalancheShapes
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public



---

## AvalancheTag

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheTag

**Contents:**
- AvalancheTag
- Navigation
- Classes
- Structs



---

## AvalancheText

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheText

**Contents:**
- AvalancheText
- Navigation
- Classes
- Structs
- Enums
  - Public
- Variables
  - Public
- Functions
  - Public

void UE::Ava::FontUtilities::GetFontName ( const UFont* InFont, FString& OutFontName )



---

## AvalancheTransitionEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheTransitionEditor

**Contents:**
- AvalancheTransitionEditor
- Navigation
- Classes
- Structs
- Interfaces
- Variables
  - Public
- Functions
  - Public

FGuid UE::AvaTransitionEditor::ColorId_In ( 0x1DDBC788, 0xD5EB400E, 0xBB71E5DA, 0xB27A784D )

FGuid UE::AvaTransitionEditor::ColorId_Out ( 0xE549EFA0, 0xDEFF45A7, 0xA8D907AF, 0xDB8F7643 )



---

## AvalancheTransition

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheTransition

**Contents:**
- AvalancheTransition
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public
  - Static

ENUM_CLASS_FLAGS ( EAvaTransitionSceneFlags )

ENUM_CLASS_FLAGS ( EAvaTransitionType )

static InNodeType::FInstanceDataType * UE::AvaTransition::TryGetInstanceData ( const InNodeType& InNode, FStateTreeDataView InInstanceDataView )



---

## AvalancheViewport

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvalancheViewport

**Contents:**
- AvalancheViewport
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

ENUM_CLASS_FLAGS ( EAvaViewportSnapState )



---

## Avalanche

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Avalanche

**Contents:**
- Avalanche
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

_Pragma ( "message("Use AvaAttributeContainer.h instead" " Please update your code to the new API before up... )

EAvaDepthAlignment GetDAlignment ( AvaAlignment InAlignment )

EAvaHorizontalAlignment GetHAlignment ( AvaAlignment InAlignment )

FVector GetLocationFromAlignment ( AvaAlignment InAlignment, FVector Size3D )

EAvaVerticalAlignment GetVAlignment ( AvaAlignment InAlignment )

AvaAlignment MakeAlignment ( EAvaDepthAlignment Depth, EAvaHorizontalAlignment Horizontal, EAvaVerticalAlignment Vertical )

auto ToUnderlyingType ( Enum Val )



---

## AVCodecsCoreRHI

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AVCodecsCoreRHI

**Contents:**
- AVCodecsCoreRHI
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

DECLARE_TYPEID ( FVideoContextRHI, AVCODECSCORERHI_API )

DECLARE_TYPEID ( FVideoResourceRHI, AVCODECSCORERHI_API )



---

## AVCodecsCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AVCodecsCore

**Contents:**
- AVCodecsCore
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

TUniquePtr< FScalableVideoController > CreateScalabilityStructure ( EScalabilityMode Name )

bool operator!= ( EPixelFormat LHS, EVideoFormat RHS )

bool operator!= ( EVideoFormat LHS, EPixelFormat RHS )

bool operator== ( EPixelFormat LHS, EVideoFormat RHS )

bool operator== ( EVideoFormat LHS, EPixelFormat RHS )

TOptional< EScalabilityMode > ScalabilityModeFromString ( const FString& ModeString )

TOptional< FScalableVideoController::FStreamLayersConfig > ScalabilityStructureConfig ( EScalabilityMode Name )

FString ToString ( EAVResult Result )

int32 UE::AVCodecCore::H264::EBSPtoRBSP ( uint8* OutBuf, const uint8* InBuf, int32 NumBytesIn )

EH264ConstraintFlag UE::AVCodecCore::H264::operator& ( EH264ConstraintFlag const& lhs, EH264ConstraintFlag const& rhs )

uint8 UE::AVCodecCore::H264::operator& ( uint8 const& lhs, EH264ConstraintFlag const& rhs )

EH264ConstraintFlag UE::AVCodecCore::H264::operator| ( EH264ConstraintFlag const& lhs, EH264ConstraintFlag const& rhs )

EH264ConstraintFlag UE::AVCodecCore::H264::operator|= ( EH264ConstraintFlag const& lhs, EH264ConstraintFlag const& rhs )

bool UE::AVCodecCore::H264::operator== ( EH264ConstraintFlag lhs, EH264ConstraintFlag rhs )

void UE::AVCodecCore::H264::ScaleListToWeightScale ( const bool bIsFrame, const uint8* ScalingList, const uint8 ListSize, uint8* OutWeightList )

bool UE::AVCodecCore::H265::CheckProfileCompatabilityFlag ( uint32 const& profile_compatibility_flag, EH265ProfileIDC const& H265ProfileIdc )

int32 UE::AVCodecCore::H265::EBSPtoRBSP ( uint8* OutBuf, const uint8* InBuf, int32 NumBytesIn )

EH265ConstraintFlag UE::AVCodecCore::H265::operator& ( EH265ConstraintFlag const& lhs, EH265ConstraintFlag const& rhs )

uint8 UE::AVCodecCore::H265::operator& ( uint16 const& lhs, EH265ConstraintFlag const& rhs )

EH265ConstraintFlag UE::AVCodecCore::H265::operator| ( EH265ConstraintFlag const& lhs, EH265ConstraintFlag const& rhs )

EH265ConstraintFlag UE::AVCodecCore::H265::operator|= ( EH265ConstraintFlag const& lhs, EH265ConstraintFlag const& rhs )

bool UE::AVCodecCore::H265::operator== ( EH265ConstraintFlag lhs, EH265ConstraintFlag rhs )

bool UE::AVCodecCore::VP8::operator! ( EBufferFlags E )

bool UE::AVCodecCore::VP8::operator! ( EBufferType E )

EBufferFlags UE::AVCodecCore::VP8::operator& ( EBufferFlags Lhs, EBufferFlags Rhs )

EBufferType UE::AVCodecCore::VP8::operator& ( EBufferType Lhs, EBufferType Rhs )

EBufferFlags & UE::AVCodecCore::VP8::operator&= ( EBufferFlags& Lhs, EBufferFlags Rhs )

EBufferType & UE::AVCodecCore::VP8::operator&= ( EBufferType& Lhs, EBufferType Rhs )

EBufferFlags UE::AVCodecCore::VP8::operator^ ( EBufferFlags Lhs, EBufferFlags Rhs )

EBufferType UE::AVCodecCore::VP8::operator^ ( EBufferType Lhs, EBufferType Rhs )

EBufferFlags & UE::AVCodecCore::VP8::operator^= ( EBufferFlags& Lhs, EBufferFlags Rhs )

EBufferType & UE::AVCodecCore::VP8::operator^= ( EBufferType& Lhs, EBufferType Rhs )

EBufferFlags UE::AVCodecCore::VP8::operator| ( EBufferFlags Lhs, EBufferFlags Rhs )

EBufferType UE::AVCodecCore::VP8::operator| ( EBufferType Lhs, EBufferType Rhs )

EBufferFlags & UE::AVCodecCore::VP8::operator|= ( EBufferFlags& Lhs, EBufferFlags Rhs )

EBufferType & UE::AVCodecCore::VP8::operator|= ( EBufferType& Lhs, EBufferType Rhs )

EBufferFlags UE::AVCodecCore::VP8::operator~ ( EBufferFlags E )

EBufferType UE::AVCodecCore::VP8::operator~ ( EBufferType E )



---

## AvfMediaFactory

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvfMediaFactory

**Contents:**
- AvfMediaFactory
- Navigation
- Classes



---

## AvidDNxMedia

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AvidDNxMedia

**Contents:**
- AvidDNxMedia
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public



---

## AxFImporter

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/AxFImporter

**Contents:**
- AxFImporter
- Navigation
- Interfaces



---

## BackChannel

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/BackChannel

**Contents:**
- BackChannel
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## BaseCharacterFXEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/BaseCharacterFXEditor

**Contents:**
- BaseCharacterFXEditor
- Navigation
- Classes



---

## BinkMediaPlayer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/BinkMediaPlayer

**Contents:**
- BinkMediaPlayer
- Navigation
- Classes
- Enums
  - Public
- Variables
  - Public
- Functions
  - Public

FString BinkUE4CookOnTheFlyPath ( FString path, const TCHAR* filename )



---

## BlackmagicCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/BlackmagicCore

**Contents:**
- BlackmagicCore
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Functions
  - Public

bool BlackmagicDesign::operator!= ( const ReferencePtr< T >& lhs, std::nullptr_t rhs )

bool BlackmagicDesign::operator!= ( std::nullptr_t lhs, const ReferencePtr< T >& rhs )

bool BlackmagicDesign::operator== ( const ReferencePtr< T >& lhs, std::nullptr_t rhs )

bool BlackmagicDesign::operator== ( std::nullptr_t lhs, const ReferencePtr< T >& rhs )

void BlackmagicDesign::SetLoggingCallbacks ( LoggingCallbackPtr LogInfoFunc, LoggingCallbackPtr LogWarningFunc, LoggingCallbackPtr LogErrorFunc, LoggingCallbackPtr LogVerboseFunc )



---

## BlackmagicMediaOutput

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/BlackmagicMediaOutput

**Contents:**
- BlackmagicMediaOutput
- Navigation
- Classes
- Enums
  - Public



---

## BlackmagicMedia

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/BlackmagicMedia

**Contents:**
- BlackmagicMedia
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## BlankPlugin

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/BlankPlugin

**Contents:**
- BlankPlugin
- Navigation
- Interfaces



---

## BlendSpaceMotionAnalysis

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/BlendSpaceMotionAnalysis

**Contents:**
- BlendSpaceMotionAnalysis
- Navigation
- Classes
- Enums
  - Public
- Functions
  - Public

bool CalculateLocomotion ( float& Result, const UBlendSpace& BlendSpace, const ULocomotionAnalysisProperties* AnalysisProperties, const UAnimSequence& Animation, const float RateScale )

bool CalculateRootMotion ( float& Result, const UBlendSpace& BlendSpace, const URootMotionAnalysisProperties* AnalysisProperties, const UAnimSequence& Animation, const float RateScale )



---

## BlendStackEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/BlendStackEditor

**Contents:**
- BlendStackEditor
- Navigation
- Classes
- Interfaces



---

## BlendStack

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/BlendStack

**Contents:**
- BlendStack
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## BlueprintFileUtils

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/BlueprintFileUtils

**Contents:**
- BlueprintFileUtils
- Navigation
- Classes



---

## BlueprintHeaderView

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/BlueprintHeaderView

**Contents:**
- BlueprintHeaderView
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## BlueprintMaterialTextureNodes

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/BlueprintMaterialTextureNodes

**Contents:**
- BlueprintMaterialTextureNodes
- Navigation
- Classes



---

## BlueprintSnapNodes

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/BlueprintSnapNodes

**Contents:**
- BlueprintSnapNodes
- Navigation
- Classes



---

## BlueprintStats

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/BlueprintStats

**Contents:**
- BlueprintStats
- Navigation
- Interfaces



---

## BodyIntersectIKOp

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/BodyIntersectIKOp

**Contents:**
- BodyIntersectIKOp
- Navigation
- Classes
- Structs



---

## Bridge

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Bridge

**Contents:**
- Bridge
- Navigation
- Interfaces



---

## BspMode

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/BspMode

**Contents:**
- BspMode
- Navigation
- Classes
- Interfaces



---

## Buoyancy

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Buoyancy

**Contents:**
- Buoyancy
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

bool BuoyancyAlgorithms::ComputeSubmergedVolume ( FBuoyancyParticleData& ParticleData, const Chaos::FGeometryParticleHandle* ParticleA, const Chaos::FGeometryParticleHandle* ParticleB, int32 NumSubdivisions, float MinVolume, float& SubmergedVol, Chaos::FVec3& SubmergedCoM )

bool BuoyancyAlgorithms::ComputeSubmergedVolume ( FBuoyancyParticleData& ParticleData, const Chaos::FPBDRigidsEvolutionGBF& Evolution, const Chaos::FGeometryParticleHandle* ParticleA, const Chaos::FGeometryParticleHandle* ParticleB, int32 NumSubdivisions, float MinVolume, float& SubmergedVol, Chaos::FVec3& SubmergedCoM, float& TotalVol )

bool operator! ( EBuoyancyEventFlags E )

EBuoyancyEventFlags operator& ( EBuoyancyEventFlags Lhs, EBuoyancyEventFlags Rhs )

EBuoyancyEventFlags & operator&= ( EBuoyancyEventFlags& Lhs, EBuoyancyEventFlags Rhs )

EBuoyancyEventFlags operator^ ( EBuoyancyEventFlags Lhs, EBuoyancyEventFlags Rhs )

EBuoyancyEventFlags & operator^= ( EBuoyancyEventFlags& Lhs, EBuoyancyEventFlags Rhs )

EBuoyancyEventFlags operator| ( EBuoyancyEventFlags Lhs, EBuoyancyEventFlags Rhs )

EBuoyancyEventFlags & operator|= ( EBuoyancyEventFlags& Lhs, EBuoyancyEventFlags Rhs )

EBuoyancyEventFlags operator~ ( EBuoyancyEventFlags E )



---

## CableComponent

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CableComponent

**Contents:**
- CableComponent
- Navigation
- Classes
- Structs



---

## CacheTrackRecorder

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CacheTrackRecorder

**Contents:**
- CacheTrackRecorder
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## CADInterfaces

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CADInterfaces

**Contents:**
- CADInterfaces
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

A3DAsmPartDefinition * CADLibrary::TechSoftUtils::CreatePart ( TArray< A3DRiRepresentationItem* >& RepresentationItems )

A3DRiRepresentationItem * CADLibrary::TechSoftUtils::CreateRIBRep ( A3DTopoShell* TopoShellPtr )

A3DTopoEdge * CADLibrary::TechSoftUtils::CreateTopoEdge()

A3DTopoFace * CADLibrary::TechSoftUtils::CreateTopoFaceWithNaturalLoop ( A3DSurfBase* CarrierSurface )

A3DCrvNurbs * CADLibrary::TechSoftUtils::CreateTrimNurbsCurve ( A3DCrvNurbs* CurveNurbsPtr, double UMin, double UMax, bool bIs2D )

int32 CADLibrary::TechSoftUtils::SetEntityGraphicsColor ( A3DEntity* InEntity, FColor Color )



---

## CADKernelSurface

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CADKernelSurface

**Contents:**
- CADKernelSurface
- Navigation
- Classes



---

## CADLibrary

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CADLibrary

**Contents:**
- CADLibrary
- Navigation
- Classes
- Structs



---

## CADTools

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CADTools

**Contents:**
- CADTools
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Functions
  - Public
  - Static

FString CADLibrary::BuildCacheFilePath ( const TCHAR* CachePath, const TCHAR* Folder, uint32 BodyHash, const EMesher Mesher )

FString CADLibrary::BuildCadCachePath ( const TCHAR* CachePath, uint32 FileHash )

bool CADLibrary::operator! ( ESewOption E )

ESewOption CADLibrary::operator& ( ESewOption Lhs, ESewOption Rhs )

ESewOption & CADLibrary::operator&= ( ESewOption& Lhs, ESewOption Rhs )

ESewOption CADLibrary::operator^ ( ESewOption Lhs, ESewOption Rhs )

ESewOption & CADLibrary::operator^= ( ESewOption& Lhs, ESewOption Rhs )

ESewOption CADLibrary::operator| ( ESewOption Lhs, ESewOption Rhs )

ESewOption & CADLibrary::operator|= ( ESewOption& Lhs, ESewOption Rhs )

ESewOption CADLibrary::operator~ ( ESewOption E )

static ESewOption CADLibrary::SewOption::GetFromImportParameters()



---

## CameraCalibrationCoreEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CameraCalibrationCoreEditor

**Contents:**
- CameraCalibrationCoreEditor
- Navigation
- Classes
- Interfaces



---

## CameraCalibrationCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CameraCalibrationCore

**Contents:**
- CameraCalibrationCore
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## CameraShakePreviewer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CameraShakePreviewer

**Contents:**
- CameraShakePreviewer
- Navigation
- Classes
- Structs
- Typedefs



---

## CaptureDataConverter

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CaptureDataConverter

**Contents:**
- CaptureDataConverter
- Navigation
- Classes
- Structs
- Typedefs



---

## CaptureDataCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CaptureDataCore

**Contents:**
- CaptureDataCore
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

TArray< FFrameRange > PackIntoFrameRanges ( TArray< FFrameNumber > InFrameNumbers )



---

## CaptureDataEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CaptureDataEditor

**Contents:**
- CaptureDataEditor
- Navigation
- Classes
- Structs



---

## CaptureDataUtils

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CaptureDataUtils

**Contents:**
- CaptureDataUtils
- Navigation
- Classes
- Functions
  - Public

FFrameRate ConvertFrameRate ( double InFrameRate )

FTimecode ParseTimecode ( const FString& InTimecodeString )



---

## CaptureManagerEditorSettings

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CaptureManagerEditorSettings

**Contents:**
- CaptureManagerEditorSettings
- Navigation
- Classes
- Structs
- Constants



---

## CaptureManagerEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CaptureManagerEditor

**Contents:**
- CaptureManagerEditor
- Navigation
- Classes



---

## CaptureManagerMediaRW

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CaptureManagerMediaRW

**Contents:**
- CaptureManagerMediaRW
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

bool UE::CaptureManager::operator== ( const FCoordinateSystem& InLeft, const FCoordinateSystem& InRight )



---

## CaptureManagerPipeline

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CaptureManagerPipeline

**Contents:**
- CaptureManagerPipeline
- Navigation
- Classes
- Enums
  - Public



---

## CaptureManagerSettings

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CaptureManagerSettings

**Contents:**
- CaptureManagerSettings
- Navigation
- Classes
- Structs
- Constants



---

## CaptureManagerStyle

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CaptureManagerStyle

**Contents:**
- CaptureManagerStyle
- Navigation
- Classes



---

## CaptureManagerTakeMetadata

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CaptureManagerTakeMetadata

**Contents:**
- CaptureManagerTakeMetadata
- Navigation
- Classes
- Structs
- Functions
  - Public

TOptional< FTakeMetadataSerializerError > SerializeTakeMetadata ( const FString& InFilePath, const FTakeMetadata& InMetadata )



---

## CaptureManagerUnrealEndpoint

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CaptureManagerUnrealEndpoint

**Contents:**
- CaptureManagerUnrealEndpoint
- Navigation
- Classes
- Structs



---

## CaptureProtocolStack

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CaptureProtocolStack

**Contents:**
- CaptureProtocolStack
- Navigation
- Classes
- Structs



---

## CaptureUtils

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CaptureUtils

**Contents:**
- CaptureUtils
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

static void UE::CaptureManager::Private::ExecuteDelegate ( TDelegate< void(Args...)> InDelegate, EDelegateExecutionThread InThread, Args&&... InArgs )

static ENamedThreads::Type UE::CaptureManager::Private::GetThreadType ( EDelegateExecutionThread InThread )



---

## CascadeToNiagaraConverter

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CascadeToNiagaraConverter

**Contents:**
- CascadeToNiagaraConverter
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## Cascade

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Cascade

**Contents:**
- Cascade
- Navigation
- Classes
- Structs
- Interfaces
- Variables
  - Public



---

## CelestialVaultEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CelestialVaultEditor

**Contents:**
- CelestialVaultEditor
- Navigation
- Classes



---

## CelestialVault

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CelestialVault

**Contents:**
- CelestialVault
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## ChangelistReview

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChangelistReview

**Contents:**
- ChangelistReview
- Navigation
- Classes
- Structs
- Enums
  - Public
- Variables
  - Public



---

## ChangeWebBrowserUserAgent

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChangeWebBrowserUserAgent

**Contents:**
- ChangeWebBrowserUserAgent
- Navigation



---

## ChaosCachingEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosCachingEditor

**Contents:**
- ChaosCachingEditor
- Navigation
- Classes
- Interfaces



---

## ChaosCachingUSD

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosCachingUSD

**Contents:**
- ChaosCachingUSD
- Navigation
- Classes



---

## ChaosCaching

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosCaching

**Contents:**
- ChaosCaching
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## ChaosClothAssetDataflowNodes

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosClothAssetDataflowNodes

**Contents:**
- ChaosClothAssetDataflowNodes
- Navigation
- Classes
- Structs
- Enums
  - Public
- Constants
- Variables
  - Public
- Functions

void CalculateFinalSecondarySet ( const TSet< int32 >& InputSet, TSet< int32 >& FinalSet ) const

void CalculateFinalSet ( const TSet< int32 >& InputSet, TSet< int32 >& FinalSet ) const

virtual void Evaluate ( UE::Dataflow::FContext& Context, const FDataflowOutput* Out ) const

FChaosClothAssetAddWeightMapNode ( const UE::Dataflow::FNodeParameters& InParam, FGuid InGuid )

FChaosClothAssetAttributeNode ( const UE::Dataflow::FNodeParameters& InParam, FGuid InGuid )

FChaosClothAssetMergeClothCollectionsNode ( const UE::Dataflow::FNodeParameters& InParam, FGuid InGuid )

FChaosClothAssetProxyDeformerNode ( const UE::Dataflow::FNodeParameters& InParam, FGuid InGuid )

FChaosClothAssetRemeshNode ( const UE::Dataflow::FNodeParameters& InParam, FGuid InGuid )

FChaosClothAssetSelectionNode ( const UE::Dataflow::FNodeParameters& InParam, FGuid InGuid )

FChaosClothAssetSimulationLongRangeAttachmentConfigNode ( const UE::Dataflow::FNodeParameters& InParam, FGuid InGuid )

FChaosClothAssetSimulationSelfCollisionConfigNode ( const UE::Dataflow::FNodeParameters& InParam, FGuid InGuid )

FChaosClothAssetSkeletalMeshImportNode ( const UE::Dataflow::FNodeParameters& InParam, FGuid InGuid )

FChaosClothAssetStaticMeshImportNode ( const UE::Dataflow::FNodeParameters& InParam, FGuid InGuid )

FChaosClothAssetTerminalNode ( const UE::Dataflow::FNodeParameters& InParam, FGuid InGuid )

FChaosClothAssetUSDImportNode ( const UE::Dataflow::FNodeParameters& InParam, FGuid InGuid )

const TArray< FName > & GetCachedCollectionGroupNames ()

const TArray< FName > & GetCachedCollectionGroupNames ()

FName GetInputName ( UE::Dataflow::FContext& Context ) const

virtual void Serialize ( FArchive& Ar )

void SetIndices ( const TSet< int32 >& InputSet, const TSet< int32 >& FinalSet )

void SetSecondaryIndices ( const TSet< int32 >& InputSet, const TSet< int32 >& FinalSet )

static bool ImportFromFile ( const FString& UsdPath, const FString& AssetPath, const bool bImportSimMesh, const TSharedRef< FManagedArrayCollection >& OutClothCollection, FString& OutPackagePath, FText& OutErrorText )

static TUniquePtr< class FToolCommandChange > MakeWeightMapNodeChange ( const FChaosClothAssetAddWeightMapNode& Node )



---

## ChaosClothAssetEditorTools

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosClothAssetEditorTools

**Contents:**
- ChaosClothAssetEditorTools
- Navigation
- Classes
- Interfaces



---

## ChaosClothAssetEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosClothAssetEditor

**Contents:**
- ChaosClothAssetEditor
- Navigation
- Classes



---

## ChaosClothAssetEngine

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosClothAssetEngine

**Contents:**
- ChaosClothAssetEngine
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Constants
- Variables
  - Public

ENUM_CLASS_FLAGS ( EClothAssetAsyncProperties )



---

## ChaosClothAssetTools

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosClothAssetTools

**Contents:**
- ChaosClothAssetTools
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## ChaosClothAsset

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosClothAsset

**Contents:**
- ChaosClothAsset
- Navigation
- Classes
- Structs
- Enums
  - Public
- Variables
  - Public
- Functions
  - Public

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::CustomResizingRegionSet ( TEXT("CustomResizingRegionSet") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::CustomResizingRegionType ( TEXT("CustomResizingRegionType") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::FabricBendingStiffness ( TEXT("FabricBendingStiffness") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::FabricBucklingRatio ( TEXT("FabricBucklingRatio") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::FabricBucklingStiffness ( TEXT("FabricBucklingStiffness") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::FabricCollisionThickness ( TEXT("FabricollisionThickness") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::FabricDamping ( TEXT("FabricClothDamping") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::FabricDensity ( TEXT("FabricClothDensity") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::FabricFriction ( TEXT("FabricClothFriction") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::FabricLayer ( TEXT("FabricLayer") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::FabricPressure ( TEXT("FabricPressure") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::FabricStretchStiffness ( TEXT("FabricStretchStiffness") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::PhysicsAssetPathName ( TEXT("PhysicsAssetPathName") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::PhysicsAssetSoftObjectPathName ( TEXT("PhysicsAssetSoftObjectPathName") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::PreResizedSimPosition3D ( TEXT("PreResizedSimPosition3D") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::ReferenceBoneName ( TEXT("ReferenceBoneName") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderBoneIndices ( TEXT("RenderBoneIndices") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderBoneWeights ( TEXT("RenderBoneWeights") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderColor ( TEXT("RenderColor") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderCustomResizingBlend ( TEXT("RenderCustomResizingBlend") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderDeformerNormalBaryCoordsAndDist ( TEXT("RenderDeformerNormalBaryCoordsAndDist") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderDeformerNumInfluences ( TEXT("RenderDeformerNumInfluences") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderDeformerPositionBaryCoordsAndDist ( TEXT("RenderDeformerPositionBaryCoordsAndDist") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderDeformerSimIndices3D ( TEXT("RenderDeformerSimIndices3D") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderDeformerSkinningBlend ( TEXT("RenderDeformerSkinningBlend") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderDeformerTangentBaryCoordsAndDist ( TEXT("RenderDeformerTangentBaryCoordsAndDist") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderDeformerWeight ( TEXT("RenderDeformerWeight") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderFacesEnd ( TEXT("RenderFacesEnd") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderFacesStart ( TEXT("RenderFacesStart") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderIndices ( TEXT("RenderIndices") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderMaterialPathName ( TEXT("RenderMaterialPathName") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderMaterialSoftObjectPathName ( TEXT("RenderMaterialSoftObjectPathName") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderNormal ( TEXT("RenderNormal") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderPosition ( TEXT("RenderPosition") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderTangentU ( TEXT("RenderTangentU") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderTangentV ( TEXT("RenderTangentV") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderUVs ( TEXT("RenderUVs") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderVerticesEnd ( TEXT("RenderVerticesEnd") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::RenderVerticesStart ( TEXT("RenderVerticesStart") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SeamStitch2DEndIndices ( TEXT("SeamStitch2DEndIndices") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SeamStitch3DIndex ( TEXT("SeamStitch3DIndex") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SeamStitchEnd ( TEXT("SeamStitchEnd") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SeamStitchLookup ( TEXT("SeamStitchLookup") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SeamStitchStart ( TEXT("SeamStitchStart") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimAccessoryMeshBoneIndicesAttribute ( TEXT("SimAccessoryMeshBoneIndicesAttribute") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimAccessoryMeshBoneIndicesPrefix ( TEXT("SimAccessoryMeshBoneIndices") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimAccessoryMeshBoneWeightsAttribute ( TEXT("SimAccessoryMeshBoneWeightsAttribute") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimAccessoryMeshBoneWeightsPrefix ( TEXT("SimAccessoryMeshBoneWeights") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimAccessoryMeshName ( TEXT("SimAccessoryMeshName") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimAccessoryMeshNormalAttribute ( TEXT("SimAccessoryMeshNormalAttribute") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimAccessoryMeshNormalPrefix ( TEXT("SimAccessoryMeshNormal") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimAccessoryMeshPosition3DAttribute ( TEXT("SimAccessoryMeshPosition3DAttribute") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimAccessoryMeshPosition3DPrefix ( TEXT("SimAccessoryMeshPosition3D") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimBoneIndices ( TEXT("SimBoneIndices") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimBoneWeights ( TEXT("SimBoneWeights") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimCustomResizingBlend ( TEXT("SimCustomResizingBlend") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimFacesEnd ( TEXT("SimFacesEnd") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimFacesStart ( TEXT("SimFacesStart") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimImportVertexID ( TEXT("SimImportVertexID") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimIndices2D ( TEXT("SimIndices2D") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimIndices3D ( TEXT("SimIndices3D") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimMorphTargetName ( TEXT("SimMorphTargetName") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimMorphTargetPositionDelta ( TEXT("SimMorphTargetPositionDelta") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimMorphTargetSimVertex3DIndex ( TEXT("SimMorphTargetSimVertex3DIndex") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimMorphTargetTangentZDelta ( TEXT("SimMorphTargetTangentZDelta") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimMorphTargetVerticesEnd ( TEXT("SimMorphTargetVerticesEnd") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimMorphTargetVerticesStart ( TEXT("SimMorphTargetVerticesStart") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimNormal ( TEXT("SimNormal") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimPatternFabric ( TEXT("SimPatternFabric") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimPosition2D ( TEXT("SimPosition2D") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimPosition3D ( TEXT("SimPosition3D") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimVertex2DLookup ( TEXT("SimVertex2DLookup") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimVertex3DLookup ( TEXT("SimVertex3DLookup") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimVertices2DEnd ( TEXT("SimVertices2DEnd") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SimVertices2DStart ( TEXT("SimVertices2DStart") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SkeletalMeshPathName ( TEXT("SkeletalMeshPathName") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SkeletalMeshSoftObjectPathName ( TEXT("SkeletalMeshSoftObjectPathName") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SolverAirDamping ( TEXT("SolverAirDamping") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SolverGravity ( TEXT("SolverGravity") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SolverSubSteps ( TEXT("SolverSubSteps") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::SolverTimeStep ( TEXT("SolverTimeStep") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::TetherKinematicIndex ( TEXT("TetherKinematicIndex") )

const FName UE::Chaos::ClothAsset::ClothCollectionAttribute::TetherReferenceLength ( TEXT("TetherReferenceLength") )

bool UE::Chaos::ClothAsset::operator! ( EClothCollectionExtendedSchemas E )

EClothCollectionExtendedSchemas UE::Chaos::ClothAsset::operator& ( EClothCollectionExtendedSchemas Lhs, EClothCollectionExtendedSchemas Rhs )

EClothCollectionExtendedSchemas & UE::Chaos::ClothAsset::operator&= ( EClothCollectionExtendedSchemas& Lhs, EClothCollectionExtendedSchemas Rhs )

EClothCollectionExtendedSchemas UE::Chaos::ClothAsset::operator^ ( EClothCollectionExtendedSchemas Lhs, EClothCollectionExtendedSchemas Rhs )

EClothCollectionExtendedSchemas & UE::Chaos::ClothAsset::operator^= ( EClothCollectionExtendedSchemas& Lhs, EClothCollectionExtendedSchemas Rhs )

EClothCollectionExtendedSchemas UE::Chaos::ClothAsset::operator| ( EClothCollectionExtendedSchemas Lhs, EClothCollectionExtendedSchemas Rhs )

EClothCollectionExtendedSchemas & UE::Chaos::ClothAsset::operator|= ( EClothCollectionExtendedSchemas& Lhs, EClothCollectionExtendedSchemas Rhs )

EClothCollectionExtendedSchemas UE::Chaos::ClothAsset::operator~ ( EClothCollectionExtendedSchemas E )



---

## ChaosClothEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosClothEditor

**Contents:**
- ChaosClothEditor
- Navigation
- Classes



---

## ChaosCloth

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosCloth

**Contents:**
- ChaosCloth
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

virtual Chaos::~FClothingSimulation()

void Chaos::DebugDrawPhysMeshShaded ( FPrimitiveDrawInterface* PDI ) const

void Chaos::DisableGravityOverride()

FClothingSimulationCloth * Chaos::GetCloth ( int32 ClothId )

const FClothVisualizationNoGC * Chaos::GetClothVisualization()

virtual int32 Chaos::GetNumCloths()

virtual int32 Chaos::GetNumDynamicParticles()

virtual int32 Chaos::GetNumIterations()

virtual int32 Chaos::GetNumKinematicParticles()

virtual int32 Chaos::GetNumSubsteps()

virtual float Chaos::GetSimulationTime()

FClothingSimulationSolver * Chaos::GetSolver()

virtual bool Chaos::IsTeleported()

void Chaos::RefreshClothConfig ( const IClothingSimulationContext* InContext )

void Chaos::RefreshPhysicsAsset()

void Chaos::SetGravityOverride ( const FVector& InGravityOverride )

virtual void Chaos::AddExternalCollisions ( const FClothCollisionData& InData )

virtual void Chaos::AppendSimulationData ( TMap< int32, FClothSimulData >& OutData, const USkeletalMeshComponent* InOwnerComponent, const USkinnedMeshComponent* InOverrideComponent ) const

virtual void Chaos::ClearExternalCollisions()

virtual void Chaos::CreateActor ( USkeletalMeshComponent* InOwnerComponent, const UClothingAssetBase* InAsset, int32 SimDataIndex )

virtual IClothingSimulationContext * Chaos::CreateContext()

virtual void Chaos::DestroyActors()

virtual void Chaos::DestroyContext ( IClothingSimulationContext* InContext )

virtual void Chaos::EndCreateActor()

virtual void Chaos::FillContextAndPrepareTick ( const USkeletalMeshComponent* InComponent, float InDeltaTime, IClothingSimulationContext* InOutContext, bool bIsInitialization, bool bForceTeleportResetOnly )

virtual void Chaos::ForceClothNextUpdateTeleportAndReset_AnyThread()

virtual FBoxSphereBounds Chaos::GetBounds ( const USkeletalMeshComponent* InOwnerComponent ) const

virtual void Chaos::GetCollisions ( FClothCollisionData& OutCollisions, bool bIncludeExternal ) const

virtual void Chaos::HardResetSimulation ( const IClothingSimulationContext* InContext )

virtual void Chaos::Initialize()

virtual bool Chaos::ShouldSimulateLOD ( int32 OwnerLODIndex ) const

virtual void Chaos::Shutdown()

virtual void Chaos::Simulate_AnyThread ( const IClothingSimulationContext* InContext )



---

## ChaosFleshDeprecatedNodes

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosFleshDeprecatedNodes

**Contents:**
- ChaosFleshDeprecatedNodes
- Navigation
- Structs
- Interfaces



---

## ChaosFleshEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosFleshEditor

**Contents:**
- ChaosFleshEditor
- Navigation
- Classes
- Interfaces
- Typedefs



---

## ChaosFleshEngine

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosFleshEngine

**Contents:**
- ChaosFleshEngine
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

bool ChaosFlesh::ReadGEO ( const std::string& filename, TMap< FString, int32 >& IntVars, TMap< FString, TArray< int32 > >& IntVectorVars, TMap< FString, TArray< float > >& FloatVectorVars, TMap< FString, TPair< TArray< std::string >, TArray< int32 > > >& IndexedStringVars, std::ostream* errorStream )



---

## ChaosFleshNodes

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosFleshNodes

**Contents:**
- ChaosFleshNodes
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## ChaosFlesh

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosFlesh

**Contents:**
- ChaosFlesh
- Navigation
- Classes
- Structs
- Interfaces
- Functions
  - Public

void ComputeHexMeshFaces ( const TArray< int32 >& HexElements, TArray< FIntVector2 >& CommonFaces )

void ComputeMeshFaces ( const TArray< int32 >& mesh, Func1 GreaterThan, Func2 Equal, TArray< FIntVector2 >& CommonFaces, Func3 GenerateFace, int32 PointsPerFace )

void GenerateHexFaceMesh ( const TArray< int32 >& HexElements, TArray< int32 >& Faces )

void RadialHexMesh ( const FVector::FReal InnerRadius, const FVector::FReal OuterRadius, const FVector::FReal Height, const int32 RadialSample, const int32 AngularSample, const int32 VerticalSample, const FVector::FReal BulgeDistance, TArray< int32 >& HexElements, TArray< FVector >& HexVertices )

void RadialTetMesh ( const FVector::FReal InnerRadius, const FVector::FReal OuterRadius, const FVector::FReal Height, const int32 RadialSample, const int32 AngularSample, const int32 VerticalSample, const FVector::FReal BulgeDistance, TArray< FIntVector4 >& TetElements, TArray< FVector >& TetVertices )

void RegularHexMesh2TetMesh ( const TArray< FVector >& HexVertices, const TArray< int32 >& HexElements, TArray< FVector >& TetVertices, TArray< FIntVector4 >& TetElements )



---

## ChaosInsightsAnalysis

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosInsightsAnalysis

**Contents:**
- ChaosInsightsAnalysis
- Navigation
- Classes
- Structs
- Interfaces



---

## ChaosModularVehicleEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosModularVehicleEditor

**Contents:**
- ChaosModularVehicleEditor
- Navigation
- Classes
- Interfaces



---

## ChaosModularVehicleEngine

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosModularVehicleEngine

**Contents:**
- ChaosModularVehicleEngine
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Variables
  - Public
- Functions

UE_NET_DECLARE_NAMED_NETTOKEN_STRUCT_SERIALIZERS ( NetworkModularVehicleStateNetTokenData )

UE_NET_DECLARE_NAMED_NETTOKEN_STRUCT_SERIALIZERS ( ModuleInputNetTokenData, CHAOSMODULARVEHICLEENGINE_API )

static bool WriteCustomReport ( FString FileName, TArray< FString >& FileLines )

static bool WriteNetReport ( bool IsServer, const FString& FileLine )



---

## ChaosModularVehicle

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosModularVehicle

**Contents:**
- ChaosModularVehicle
- Navigation
- Classes
- Interfaces



---

## ChaosMover

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosMover

**Contents:**
- ChaosMover
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

bool operator! ( EChaosPatternAxisMaskFlags E )

EChaosPatternAxisMaskFlags operator& ( EChaosPatternAxisMaskFlags Lhs, EChaosPatternAxisMaskFlags Rhs )

EChaosPatternAxisMaskFlags & operator&= ( EChaosPatternAxisMaskFlags& Lhs, EChaosPatternAxisMaskFlags Rhs )

EChaosPatternAxisMaskFlags operator^ ( EChaosPatternAxisMaskFlags Lhs, EChaosPatternAxisMaskFlags Rhs )

EChaosPatternAxisMaskFlags & operator^= ( EChaosPatternAxisMaskFlags& Lhs, EChaosPatternAxisMaskFlags Rhs )

EChaosPatternAxisMaskFlags operator| ( EChaosPatternAxisMaskFlags Lhs, EChaosPatternAxisMaskFlags Rhs )

EChaosPatternAxisMaskFlags & operator|= ( EChaosPatternAxisMaskFlags& Lhs, EChaosPatternAxisMaskFlags Rhs )

EChaosPatternAxisMaskFlags operator~ ( EChaosPatternAxisMaskFlags E )

FMoverDataCollection & UE::ChaosMover::GetDebugSimData ( UChaosMoverSimulation* Simulation )



---

## ChaosNiagara

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosNiagara

**Contents:**
- ChaosNiagara
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## ChaosOutfitAssetEngine

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosOutfitAssetEngine

**Contents:**
- ChaosOutfitAssetEngine
- Navigation
- Classes
- Structs
- Variables
  - Public



---

## ChaosRigidAssetEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosRigidAssetEditor

**Contents:**
- ChaosRigidAssetEditor
- Navigation
- Classes



---

## ChaosRigidAssetEngine

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosRigidAssetEngine

**Contents:**
- ChaosRigidAssetEngine
- Navigation
- Classes



---

## ChaosRigidAssetNodes

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosRigidAssetNodes

**Contents:**
- ChaosRigidAssetNodes
- Navigation
- Classes
- Structs
- Functions
  - Public

void AddArrayReferences ( FReferenceCollector& Collector, const T&... Args )



---

## ChaosSolverEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosSolverEditor

**Contents:**
- ChaosSolverEditor
- Navigation
- Classes
- Interfaces



---

## ChaosUserDataPT

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosUserDataPT

**Contents:**
- ChaosUserDataPT
- Navigation
- Classes
- Structs
- Variables
  - Public



---

## ChaosVDBlueprint

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosVDBlueprint

**Contents:**
- ChaosVDBlueprint
- Navigation
- Classes



---

## ChaosVDBuiltInExtensions

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosVDBuiltInExtensions

**Contents:**
- ChaosVDBuiltInExtensions
- Navigation
- Classes



---

## ChaosVD

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosVD

**Contents:**
- ChaosVD
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Functions

FTypedElementHandle Chaos::VD::TypedElementDataUtil::AcquireTypedElementHandleForStruct ( StructDataType* ElementInstance, const bool bAllowCreate )

TTypedElementOwner< FStructTypedElementData > Chaos::VD::TypedElementDataUtil::CreateTypedElementDataForStructData ( StructDataType* InElementData )

StructDataType * Chaos::VD::TypedElementDataUtil::GetStructDataFromTypedElementHandle ( const FTypedElementHandle& InHandle, const bool bSilent )

bool operator! ( EChaosVDGeometryTransformGeneratorFlags E )

bool operator! ( EChaosVDMeshAttributesFlags E )

bool operator! ( EChaosVDUnloadRecordingFlags E )

bool operator! ( EChaosVDSceneCleanUpOptions E )

bool operator! ( EChaosVDParticleVisibilityUpdateFlags E )

bool operator! ( EChaosVDActorGeometryUpdateFlags E )

bool operator! ( EChaosVDHideParticleFlags E )

bool operator! ( EChaosVDSceneParticleDirtyFlags E )

bool operator! ( EChaosVDStreamingDirtyFlags E )

bool operator! ( EChaosVDSolverStageAccessorFlags E )

EChaosVDGeometryTransformGeneratorFlags operator& ( EChaosVDGeometryTransformGeneratorFlags Lhs, EChaosVDGeometryTransformGeneratorFlags Rhs )

EChaosVDMeshAttributesFlags operator& ( EChaosVDMeshAttributesFlags Lhs, EChaosVDMeshAttributesFlags Rhs )

EChaosVDUnloadRecordingFlags operator& ( EChaosVDUnloadRecordingFlags Lhs, EChaosVDUnloadRecordingFlags Rhs )

EChaosVDSceneCleanUpOptions operator& ( EChaosVDSceneCleanUpOptions Lhs, EChaosVDSceneCleanUpOptions Rhs )

EChaosVDParticleVisibilityUpdateFlags operator& ( EChaosVDParticleVisibilityUpdateFlags Lhs, EChaosVDParticleVisibilityUpdateFlags Rhs )

EChaosVDActorGeometryUpdateFlags operator& ( EChaosVDActorGeometryUpdateFlags Lhs, EChaosVDActorGeometryUpdateFlags Rhs )

EChaosVDHideParticleFlags operator& ( EChaosVDHideParticleFlags Lhs, EChaosVDHideParticleFlags Rhs )

EChaosVDSceneParticleDirtyFlags operator& ( EChaosVDSceneParticleDirtyFlags Lhs, EChaosVDSceneParticleDirtyFlags Rhs )

EChaosVDStreamingDirtyFlags operator& ( EChaosVDStreamingDirtyFlags Lhs, EChaosVDStreamingDirtyFlags Rhs )

EChaosVDSolverStageAccessorFlags operator& ( EChaosVDSolverStageAccessorFlags Lhs, EChaosVDSolverStageAccessorFlags Rhs )

EChaosVDGeometryTransformGeneratorFlags & operator&= ( EChaosVDGeometryTransformGeneratorFlags& Lhs, EChaosVDGeometryTransformGeneratorFlags Rhs )

EChaosVDMeshAttributesFlags & operator&= ( EChaosVDMeshAttributesFlags& Lhs, EChaosVDMeshAttributesFlags Rhs )

EChaosVDUnloadRecordingFlags & operator&= ( EChaosVDUnloadRecordingFlags& Lhs, EChaosVDUnloadRecordingFlags Rhs )

EChaosVDSceneCleanUpOptions & operator&= ( EChaosVDSceneCleanUpOptions& Lhs, EChaosVDSceneCleanUpOptions Rhs )

EChaosVDParticleVisibilityUpdateFlags & operator&= ( EChaosVDParticleVisibilityUpdateFlags& Lhs, EChaosVDParticleVisibilityUpdateFlags Rhs )

EChaosVDActorGeometryUpdateFlags & operator&= ( EChaosVDActorGeometryUpdateFlags& Lhs, EChaosVDActorGeometryUpdateFlags Rhs )

EChaosVDHideParticleFlags & operator&= ( EChaosVDHideParticleFlags& Lhs, EChaosVDHideParticleFlags Rhs )

EChaosVDSceneParticleDirtyFlags & operator&= ( EChaosVDSceneParticleDirtyFlags& Lhs, EChaosVDSceneParticleDirtyFlags Rhs )

EChaosVDStreamingDirtyFlags & operator&= ( EChaosVDStreamingDirtyFlags& Lhs, EChaosVDStreamingDirtyFlags Rhs )

EChaosVDSolverStageAccessorFlags & operator&= ( EChaosVDSolverStageAccessorFlags& Lhs, EChaosVDSolverStageAccessorFlags Rhs )

EChaosVDGeometryTransformGeneratorFlags operator^ ( EChaosVDGeometryTransformGeneratorFlags Lhs, EChaosVDGeometryTransformGeneratorFlags Rhs )

EChaosVDMeshAttributesFlags operator^ ( EChaosVDMeshAttributesFlags Lhs, EChaosVDMeshAttributesFlags Rhs )

EChaosVDUnloadRecordingFlags operator^ ( EChaosVDUnloadRecordingFlags Lhs, EChaosVDUnloadRecordingFlags Rhs )

EChaosVDSceneCleanUpOptions operator^ ( EChaosVDSceneCleanUpOptions Lhs, EChaosVDSceneCleanUpOptions Rhs )

EChaosVDParticleVisibilityUpdateFlags operator^ ( EChaosVDParticleVisibilityUpdateFlags Lhs, EChaosVDParticleVisibilityUpdateFlags Rhs )

EChaosVDActorGeometryUpdateFlags operator^ ( EChaosVDActorGeometryUpdateFlags Lhs, EChaosVDActorGeometryUpdateFlags Rhs )

EChaosVDHideParticleFlags operator^ ( EChaosVDHideParticleFlags Lhs, EChaosVDHideParticleFlags Rhs )

EChaosVDSceneParticleDirtyFlags operator^ ( EChaosVDSceneParticleDirtyFlags Lhs, EChaosVDSceneParticleDirtyFlags Rhs )

EChaosVDStreamingDirtyFlags operator^ ( EChaosVDStreamingDirtyFlags Lhs, EChaosVDStreamingDirtyFlags Rhs )

EChaosVDSolverStageAccessorFlags operator^ ( EChaosVDSolverStageAccessorFlags Lhs, EChaosVDSolverStageAccessorFlags Rhs )

EChaosVDGeometryTransformGeneratorFlags & operator^= ( EChaosVDGeometryTransformGeneratorFlags& Lhs, EChaosVDGeometryTransformGeneratorFlags Rhs )

EChaosVDMeshAttributesFlags & operator^= ( EChaosVDMeshAttributesFlags& Lhs, EChaosVDMeshAttributesFlags Rhs )

EChaosVDUnloadRecordingFlags & operator^= ( EChaosVDUnloadRecordingFlags& Lhs, EChaosVDUnloadRecordingFlags Rhs )

EChaosVDSceneCleanUpOptions & operator^= ( EChaosVDSceneCleanUpOptions& Lhs, EChaosVDSceneCleanUpOptions Rhs )

EChaosVDParticleVisibilityUpdateFlags & operator^= ( EChaosVDParticleVisibilityUpdateFlags& Lhs, EChaosVDParticleVisibilityUpdateFlags Rhs )

EChaosVDActorGeometryUpdateFlags & operator^= ( EChaosVDActorGeometryUpdateFlags& Lhs, EChaosVDActorGeometryUpdateFlags Rhs )

EChaosVDHideParticleFlags & operator^= ( EChaosVDHideParticleFlags& Lhs, EChaosVDHideParticleFlags Rhs )

EChaosVDSceneParticleDirtyFlags & operator^= ( EChaosVDSceneParticleDirtyFlags& Lhs, EChaosVDSceneParticleDirtyFlags Rhs )

EChaosVDStreamingDirtyFlags & operator^= ( EChaosVDStreamingDirtyFlags& Lhs, EChaosVDStreamingDirtyFlags Rhs )

EChaosVDSolverStageAccessorFlags & operator^= ( EChaosVDSolverStageAccessorFlags& Lhs, EChaosVDSolverStageAccessorFlags Rhs )

EChaosVDGeometryTransformGeneratorFlags operator| ( EChaosVDGeometryTransformGeneratorFlags Lhs, EChaosVDGeometryTransformGeneratorFlags Rhs )

EChaosVDMeshAttributesFlags operator| ( EChaosVDMeshAttributesFlags Lhs, EChaosVDMeshAttributesFlags Rhs )

EChaosVDUnloadRecordingFlags operator| ( EChaosVDUnloadRecordingFlags Lhs, EChaosVDUnloadRecordingFlags Rhs )

EChaosVDSceneCleanUpOptions operator| ( EChaosVDSceneCleanUpOptions Lhs, EChaosVDSceneCleanUpOptions Rhs )

EChaosVDParticleVisibilityUpdateFlags operator| ( EChaosVDParticleVisibilityUpdateFlags Lhs, EChaosVDParticleVisibilityUpdateFlags Rhs )

EChaosVDActorGeometryUpdateFlags operator| ( EChaosVDActorGeometryUpdateFlags Lhs, EChaosVDActorGeometryUpdateFlags Rhs )

EChaosVDHideParticleFlags operator| ( EChaosVDHideParticleFlags Lhs, EChaosVDHideParticleFlags Rhs )

EChaosVDSceneParticleDirtyFlags operator| ( EChaosVDSceneParticleDirtyFlags Lhs, EChaosVDSceneParticleDirtyFlags Rhs )

EChaosVDStreamingDirtyFlags operator| ( EChaosVDStreamingDirtyFlags Lhs, EChaosVDStreamingDirtyFlags Rhs )

EChaosVDSolverStageAccessorFlags operator| ( EChaosVDSolverStageAccessorFlags Lhs, EChaosVDSolverStageAccessorFlags Rhs )

EChaosVDGeometryTransformGeneratorFlags & operator|= ( EChaosVDGeometryTransformGeneratorFlags& Lhs, EChaosVDGeometryTransformGeneratorFlags Rhs )

EChaosVDMeshAttributesFlags & operator|= ( EChaosVDMeshAttributesFlags& Lhs, EChaosVDMeshAttributesFlags Rhs )

EChaosVDUnloadRecordingFlags & operator|= ( EChaosVDUnloadRecordingFlags& Lhs, EChaosVDUnloadRecordingFlags Rhs )

EChaosVDSceneCleanUpOptions & operator|= ( EChaosVDSceneCleanUpOptions& Lhs, EChaosVDSceneCleanUpOptions Rhs )

EChaosVDParticleVisibilityUpdateFlags & operator|= ( EChaosVDParticleVisibilityUpdateFlags& Lhs, EChaosVDParticleVisibilityUpdateFlags Rhs )

EChaosVDActorGeometryUpdateFlags & operator|= ( EChaosVDActorGeometryUpdateFlags& Lhs, EChaosVDActorGeometryUpdateFlags Rhs )

EChaosVDHideParticleFlags & operator|= ( EChaosVDHideParticleFlags& Lhs, EChaosVDHideParticleFlags Rhs )

EChaosVDSceneParticleDirtyFlags & operator|= ( EChaosVDSceneParticleDirtyFlags& Lhs, EChaosVDSceneParticleDirtyFlags Rhs )

EChaosVDStreamingDirtyFlags & operator|= ( EChaosVDStreamingDirtyFlags& Lhs, EChaosVDStreamingDirtyFlags Rhs )

EChaosVDSolverStageAccessorFlags & operator|= ( EChaosVDSolverStageAccessorFlags& Lhs, EChaosVDSolverStageAccessorFlags Rhs )

EChaosVDGeometryTransformGeneratorFlags operator~ ( EChaosVDGeometryTransformGeneratorFlags E )

EChaosVDMeshAttributesFlags operator~ ( EChaosVDMeshAttributesFlags E )

EChaosVDUnloadRecordingFlags operator~ ( EChaosVDUnloadRecordingFlags E )

EChaosVDSceneCleanUpOptions operator~ ( EChaosVDSceneCleanUpOptions E )

EChaosVDParticleVisibilityUpdateFlags operator~ ( EChaosVDParticleVisibilityUpdateFlags E )

EChaosVDActorGeometryUpdateFlags operator~ ( EChaosVDActorGeometryUpdateFlags E )

EChaosVDHideParticleFlags operator~ ( EChaosVDHideParticleFlags E )

EChaosVDSceneParticleDirtyFlags operator~ ( EChaosVDSceneParticleDirtyFlags E )

EChaosVDStreamingDirtyFlags operator~ ( EChaosVDStreamingDirtyFlags E )

EChaosVDSolverStageAccessorFlags operator~ ( EChaosVDSolverStageAccessorFlags E )



---

## ChaosVehiclesEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosVehiclesEditor

**Contents:**
- ChaosVehiclesEditor
- Navigation
- Classes
- Interfaces



---

## ChaosVehicles

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChaosVehicles

**Contents:**
- ChaosVehicles
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Variables
  - Public
- Functions

bool operator! ( EForceFlags E )

EForceFlags operator& ( EForceFlags Lhs, EForceFlags Rhs )

EForceFlags & operator&= ( EForceFlags& Lhs, EForceFlags Rhs )

EForceFlags operator^ ( EForceFlags Lhs, EForceFlags Rhs )

EForceFlags & operator^= ( EForceFlags& Lhs, EForceFlags Rhs )

EForceFlags operator| ( EForceFlags Lhs, EForceFlags Rhs )

EForceFlags & operator|= ( EForceFlags& Lhs, EForceFlags Rhs )

EForceFlags operator~ ( EForceFlags E )



---

## CharacterAI

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CharacterAI

**Contents:**
- CharacterAI
- Navigation
- Interfaces



---

## ChooserEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChooserEditor

**Contents:**
- ChooserEditor
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public



---

## ChooserUncooked

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChooserUncooked

**Contents:**
- ChooserUncooked
- Navigation
- Classes



---

## Chooser

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Chooser

**Contents:**
- Chooser
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

FChooserIndexArray::FIndexData * GetData ( FChooserIndexArray& Array )

uint32 GetNum ( FChooserIndexArray& Array )



---

## ChunkDownloader

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ChunkDownloader

**Contents:**
- ChunkDownloader
- Navigation
- Classes
- Structs
- Typedefs



---

## CineAssemblyToolsEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CineAssemblyToolsEditor

**Contents:**
- CineAssemblyToolsEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## CineAssemblyTools

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CineAssemblyTools

**Contents:**
- CineAssemblyTools
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## CineCameraRigs

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CineCameraRigs

**Contents:**
- CineCameraRigs
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## CineCameraSceneCapture

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CineCameraSceneCapture

**Contents:**
- CineCameraSceneCapture
- Navigation
- Classes



---

## CinematicPrestreamingEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CinematicPrestreamingEditor

**Contents:**
- CinematicPrestreamingEditor
- Navigation
- Classes
- Structs



---

## CinematicPrestreaming

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CinematicPrestreaming

**Contents:**
- CinematicPrestreaming
- Navigation
- Classes
- Structs



---

## ClonerEffectorEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ClonerEffectorEditor

**Contents:**
- ClonerEffectorEditor
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## ClonerEffectorMeshBuilder

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ClonerEffectorMeshBuilder

**Contents:**
- ClonerEffectorMeshBuilder
- Navigation
- Structs
- Enums
  - Public



---

## ClonerEffector

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ClonerEffector

**Contents:**
- ClonerEffector
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Variables
  - Public
- Functions

ADynamicMeshActor * UE::ClonerEffector::Conversion::ConvertClonerToDynamicMesh ( UCEClonerComponent* InCloner )

TArray< ADynamicMeshActor * > UE::ClonerEffector::Conversion::ConvertClonerToDynamicMeshes ( UCEClonerComponent* InCloner )

TArray< AActor * > UE::ClonerEffector::Conversion::ConvertClonerToInstancedStaticMeshes ( UCEClonerComponent* InCloner )

AStaticMeshActor * UE::ClonerEffector::Conversion::ConvertClonerToStaticMesh ( UCEClonerComponent* InCloner )

TArray< AStaticMeshActor * > UE::ClonerEffector::Conversion::ConvertClonerToStaticMeshes ( UCEClonerComponent* InCloner )

InClass * UE::ClonerEffector::Conversion::CreateAssetPackage ( const FString& InAssetPath )

UObject * UE::ClonerEffector::Conversion::CreateAssetPackage ( TSubclassOf< UObject > InAssetClass, const FString& InAssetPath )

UActorComponent * UE::ClonerEffector::Conversion::CreateRootComponent ( AActor* InActor, TSubclassOf< USceneComponent > InComponentClass, const FTransform& InWorldTransform )

bool UE::ClonerEffector::Conversion::PickAssetPath ( const FString& InDefaultPath, FString& OutPickedPath )

FCEExtensionSection UE::ClonerEffector::EditorSection::GetExtensionSectionFromClass ( UClass* InClass )

bool UE::ClonerEffector::Utilities::FilterSupportedMaterial ( UMaterialInterface*& InMaterial, UMaterialInterface* InDefaultMaterial )

bool UE::ClonerEffector::Utilities::FilterSupportedMaterials ( TArray< TWeakObjectPtr< UMaterialInterface > >& InMaterials, TArray< TWeakObjectPtr< UMaterialInterface > >& OutUnsetMaterials, UMaterialInterface* InDefaultMaterial )

AActor * UE::ClonerEffector::Utilities::FindClonerActor ( AActor* InActor )

const FText & UE::ClonerEffector::Utilities::GetMaterialWarningText()

bool UE::ClonerEffector::Utilities::IsMaterialDirtyable ( const UMaterialInterface* InMaterial )

bool UE::ClonerEffector::Utilities::IsMaterialUsageFlagSet ( const UMaterialInterface* InMaterial )

void UE::ClonerEffector::Utilities::SetActorVisibility ( AActor* InActor, bool bInVisibility, ECEClonerActorVisibility InTarget )

void UE::ClonerEffector::Utilities::ShowWarning ( const FText& InWarning )



---

## CmdLinkServer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CmdLinkServer

**Contents:**
- CmdLinkServer
- Navigation
- Classes



---

## ColorCorrectRegionsEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ColorCorrectRegionsEditor

**Contents:**
- ColorCorrectRegionsEditor
- Navigation
- Classes



---

## ColorCorrectRegions

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ColorCorrectRegions

**Contents:**
- ColorCorrectRegions
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Variables
  - Public
- Functions

BEGIN_GLOBAL_SHADER_PARAMETER_STRUCT ( FCCRRegionDataInputParameter )

RotateScale Tint Outer Intensity ExcludeStencil ColorContrast ColorGain ColorContrast ColorGain ShadowMax END_GLOBAL_SHADER_PARAMETER_STRUCT()

Rotate SHADER_PARAMETER ( FVector3f, Translate )

RotateScale SHADER_PARAMETER ( float, WhiteTemp )

RotateScale Tint SHADER_PARAMETER ( float, Inner )

RotateScale Tint Outer SHADER_PARAMETER ( float, Falloff )

RotateScale Tint Outer Intensity SHADER_PARAMETER ( float, FakeLight )

RotateScale Tint Outer Intensity ExcludeStencil SHADER_PARAMETER ( float, Invert )

RotateScale Tint Outer Intensity ExcludeStencil SHADER_PARAMETER ( FVector4f, ColorSaturation )

RotateScale Tint Outer Intensity ExcludeStencil ColorContrast SHADER_PARAMETER ( FVector4f, ColorGamma )

RotateScale Tint Outer Intensity ExcludeStencil ColorContrast ColorGain SHADER_PARAMETER ( FVector4f, ColorOffset )

RotateScale Tint Outer Intensity ExcludeStencil ColorContrast ColorGain ColorContrast ColorGain ShadowMax ColorContrast ColorGain ColorContrast ColorGain HighlightsMin SHADER_PARAMETER_RDG_TEXTURE ( Texture2D< uint >, MergedStencilTexture )

RotateScale Tint Outer Intensity ExcludeStencil ColorContrast ColorGain ColorContrast ColorGain ShadowMax ColorContrast ColorGain ColorContrast ColorGain HighlightsMin View WorkingColorSpace SHADER_PARAMETER_STRUCT ( FScreenPassTextureViewportParameters, PostProcessOutput )

RotateScale Tint Outer Intensity ExcludeStencil ColorContrast ColorGain ColorContrast ColorGain ShadowMax ColorContrast ColorGain ColorContrast ColorGain HighlightsMin View SHADER_PARAMETER_STRUCT_INCLUDE ( FSceneTextureShaderParameters, SceneTextures )



---

## ColorGradingEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ColorGradingEditor

**Contents:**
- ColorGradingEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## CommonConversationEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CommonConversationEditor

**Contents:**
- CommonConversationEditor
- Navigation
- Classes



---

## CommonConversationGraph

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CommonConversationGraph

**Contents:**
- CommonConversationGraph
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

const FLinearColor ConversationEditorColors::Action::DragMarker (

const FLinearColor ConversationEditorColors::Connection::Default (

const FLinearColor ConversationEditorColors::Debugger::DescHeader (

const FLinearColor ConversationEditorColors::Debugger::DescKeys (

const FLinearColor ConversationEditorColors::Debugger::TaskFlash (

const FLinearColor ConversationEditorColors::NodeBody::ChoiceColor (

const FLinearColor ConversationEditorColors::NodeBody::Default (

const FLinearColor ConversationEditorColors::NodeBody::EntryPoint (

const FLinearColor ConversationEditorColors::NodeBody::Error (

const FLinearColor ConversationEditorColors::NodeBody::RequirementColor (

const FLinearColor ConversationEditorColors::NodeBody::SideEffectColor (

const FLinearColor ConversationEditorColors::NodeBody::Task (

const FLinearColor ConversationEditorColors::NodeBorder::ActiveDebugging (

const FLinearColor ConversationEditorColors::NodeBorder::BrokenWithParent (

const FLinearColor ConversationEditorColors::NodeBorder::Disconnected (

const FLinearColor ConversationEditorColors::NodeBorder::HighlightAbortRange0 (

const FLinearColor ConversationEditorColors::NodeBorder::HighlightAbortRange1 (

const FLinearColor ConversationEditorColors::NodeBorder::Inactive (

const FLinearColor ConversationEditorColors::NodeBorder::InactiveDebugging (

const FLinearColor ConversationEditorColors::NodeBorder::QuickFind (

const FLinearColor ConversationEditorColors::NodeBorder::Root (

const FLinearColor ConversationEditorColors::NodeBorder::Selected (

const FLinearColor ConversationEditorColors::Pin::CompositeOnly (

const FLinearColor ConversationEditorColors::Pin::Default (

const FLinearColor ConversationEditorColors::Pin::Diff (

const FLinearColor ConversationEditorColors::Pin::Hover (

const FLinearColor ConversationEditorColors::Pin::SingleNode (

const FLinearColor ConversationEditorColors::Pin::TaskOnly (



---

## CommonConversationRuntime

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CommonConversationRuntime

**Contents:**
- CommonConversationRuntime
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Functions
  - Public

EConversationRequirementResult MergeRequirements ( EConversationRequirementResult CurrentResult, EConversationRequirementResult MergeResult )

bool operator!= ( const FConversationNodeHandle& Lhs, const FConversationNodeHandle& Rhs )

bool operator!= ( const FConversationNodeParameterPair& Lhs, const FConversationNodeParameterPair& Rhs )

bool operator!= ( const FConversationChoiceReference& Lhs, const FConversationChoiceReference& Rhs )

bool operator!= ( const FClientConversationOptionEntry& Lhs, const FClientConversationOptionEntry& Rhs )

bool operator!= ( const FClientConversationOptionEntry& Lhs, const FConversationChoiceReference& Rhs )

bool operator== ( const FConversationNodeHandle& Lhs, const FConversationNodeHandle& Rhs )

bool operator== ( const FConversationNodeParameterPair& Lhs, const FConversationNodeParameterPair& Rhs )

bool operator== ( const FConversationChoiceReference& Lhs, const FConversationChoiceReference& Rhs )

bool operator== ( const FClientConversationOptionEntry& Lhs, const FClientConversationOptionEntry& Rhs )

bool operator== ( const FClientConversationOptionEntry& Lhs, const FConversationChoiceReference& Rhs )



---

## CommonInput

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CommonInput

**Contents:**
- CommonInput
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

const TCHAR * LexToString ( ECommonInputMode Value )



---

## CommonUIEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CommonUIEditor

**Contents:**
- CommonUIEditor
- Navigation
- Classes



---

## CommonUI

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CommonUI

**Contents:**
- CommonUI
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

static ECurveEaseFunction TransitionCurveToCurveEaseFunction ( ETransitionCurve CurveType )



---

## CompositeCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CompositeCore

**Contents:**
- CompositeCore
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Constants
- Variables
  - Public



---

## CompositeEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CompositeEditor

**Contents:**
- CompositeEditor
- Navigation
- Classes



---

## Composite

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Composite

**Contents:**
- Composite
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## ComposureEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ComposureEditor

**Contents:**
- ComposureEditor
- Navigation



---

## ComposureLayersEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ComposureLayersEditor

**Contents:**
- ComposureLayersEditor
- Navigation
- Interfaces
- Enums
  - Public



---

## Composure

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Composure

**Contents:**
- Composure
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

bool operator! ( ETargetUsageFlags E )

ETargetUsageFlags operator& ( ETargetUsageFlags Lhs, ETargetUsageFlags Rhs )

ETargetUsageFlags & operator&= ( ETargetUsageFlags& Lhs, ETargetUsageFlags Rhs )

ETargetUsageFlags operator^ ( ETargetUsageFlags Lhs, ETargetUsageFlags Rhs )

ETargetUsageFlags & operator^= ( ETargetUsageFlags& Lhs, ETargetUsageFlags Rhs )

ETargetUsageFlags operator| ( ETargetUsageFlags Lhs, ETargetUsageFlags Rhs )

ETargetUsageFlags & operator|= ( ETargetUsageFlags& Lhs, ETargetUsageFlags Rhs )

ETargetUsageFlags operator~ ( ETargetUsageFlags E )



---

## ComputeFrameworkEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ComputeFrameworkEditor

**Contents:**
- ComputeFrameworkEditor
- Navigation
- Interfaces



---

## ComputeFramework

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ComputeFramework

**Contents:**
- ComputeFramework
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

void ComputeFramework::AddParamForType ( FShaderParametersMetadataBuilder& InOutBuilder, TCHAR const* InName, FShaderValueTypeHandle const& InValueType, TArray< FShaderParametersMetadata* >& OutNestedStructs )

ENUM_CLASS_FLAGS ( EComputeKernelFlags )

uint32 GetTypeHash ( const FShaderValueType& InShaderValueType )



---

## ConcertClientSharedSlate

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ConcertClientSharedSlate

**Contents:**
- ConcertClientSharedSlate
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Constants
- Variables
  - Public

void ConcertClientFrontendUtils::AppendButtons ( TSharedRef< SHorizontalBox > InHorizBox, TArrayView< const FConcertActionDefinition > InDefs )

TSharedRef< SButton > ConcertClientFrontendUtils::CreateIconButton ( const FConcertActionDefinition& InDef )

TSharedRef< SButton > ConcertClientFrontendUtils::CreateTextButton ( const FConcertActionDefinition& InDef )

virtual PRAGMA_DISABLE_DEPRECATION_WARNINGS void UE::ConcertClientSharedSlate::EnumerateSelectableItems ( TFunctionRef< EBreakBehavior(const ConcertSharedSlate::FSelectablePropertyInfo&SelectableOption)> D... ) const

virtual ConcertSharedSlate::FSourceDisplayInfo UE::ConcertClientSharedSlate::GetDisplayInfo()

virtual uint32 UE::ConcertClientSharedSlate::GetNumSelectableItems()

TAttribute< TOptional< FConcertClientInfo > > UE::ConcertClientSharedSlate::MakeClientInfoAttribute ( const TSharedRef< IConcertClient >& Client, const FGuid& ClientId )

ConcertSharedSlate::FGetOptionalClientInfo UE::ConcertClientSharedSlate::MakeClientInfoGetter ( const TSharedRef< IConcertClient >& Client )

ConcertSharedSlate::FGetClientParenthesesContent UE::ConcertClientSharedSlate::MakeGetLocalClientParenthesesContent ( const TSharedRef< IConcertClient >& Client )

ConcertSharedSlate::FIsLocalClient UE::ConcertClientSharedSlate::MakeIsLocalClientGetter ( const TSharedRef< IConcertClient >& Client )

TAttribute< TOptional< FConcertClientInfo > > UE::ConcertClientSharedSlate::MakeLocalClientInfoAttribute ( const TSharedRef< IConcertClient >& Client )

void UE::ConcertClientSharedSlate::PropertyUtils::AppendAdditionalPropertiesToAdd ( const UClass& ObjectClass, TArray< FConcertPropertyChain >& InOutPropertiesToAdd )

void UE::ConcertClientSharedSlate::PropertyUtils::AppendAdditionalPropertiesToAdd ( const FSoftClassPath& ObjectClass, TArray< FConcertPropertyChain >& InOutPropertiesToAdd )



---

## ConcertClient

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ConcertClient

**Contents:**
- ConcertClient
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## ConcertInsightsClient

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ConcertInsightsClient

**Contents:**
- ConcertInsightsClient
- Navigation
- Interfaces



---

## ConcertInsightsCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ConcertInsightsCore

**Contents:**
- ConcertInsightsCore
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

FTraceAuxiliary::EConnectionType UE::ConcertInsightsSync::ConvertTraceTargetType ( EConcertTraceTargetType ConnectionType )



---

## ConcertInsightsVisualizer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ConcertInsightsVisualizer

**Contents:**
- ConcertInsightsVisualizer
- Navigation
- Interfaces



---

## ConcertReplicationScripting

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ConcertReplicationScripting

**Contents:**
- ConcertReplicationScripting
- Navigation
- Classes
- Structs
- Functions
  - Public

uint32 GetTypeHash ( const FConcertPropertyChainWrapper& ChainWrapper )



---

## ConcertServer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ConcertServer

**Contents:**
- ConcertServer
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## ConcertSharedSlate

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ConcertSharedSlate

**Contents:**
- ConcertSharedSlate
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

FText ConcertBrowserUtils::GetServerVersionIgnoredTooltip()

TSharedRef< SWidget > ConcertBrowserUtils::MakeIconButton ( const TAttribute< const FSlateBrush* >& Icon, const TAttribute< FText >& Tooltip, const TAttribute< bool >& EnabledAttribute, const FOnClicked& OnClicked, const TAttribute< EVisibility >& Visibility )

TSharedRef< SWidget > ConcertBrowserUtils::MakeNegativeActionButton ( const TAttribute< const FSlateBrush* >& Icon, const TAttribute< FText >& Tooltip, const TAttribute< bool >& EnabledAttribute, const FOnClicked& OnClicked, const TAttribute< EVisibility >& Visibility )

TSharedRef< SWidget > ConcertBrowserUtils::MakePositiveActionButton ( const TAttribute< const FSlateBrush* >& Icon, const TAttribute< FText >& Tooltip, const TAttribute< bool >& EnabledAttribute, const FOnClicked& OnClicked, const TAttribute< EVisibility >& Visibility )

TSharedRef< SWidget > ConcertBrowserUtils::MakeServerVersionIgnoredWidget ( EConcertServerFlags InServerFlags )

void ConcertBrowserUtils::RequestItemDeletion ( IConcertSessionBrowserController& Controller, const TArray< TSharedPtr< FConcertSessionTreeItem > >& SessionItems )

TArray< TSharedPtr< ItemType > > ConcertFrontendUtils::DeepCopyArray ( const TArray< TSharedPtr< ItemType > >& InArray )

TArray< TSharedPtr< ItemType > > ConcertFrontendUtils::DeepCopyArrayAndClearSource ( TArray< TSharedPtr< ItemType > >& InOutArray )

const FSlateBrush * ConcertFrontendUtils::GetExpandableAreaBorderImage ( const SExpandableArea& Area )

void ConcertFrontendUtils::SyncArraysByPredicate ( TArray< TSharedPtr< ItemType > >& InOutArray, TArray< TSharedPtr< ItemType > >&& InNewArray, const PredFactoryType& InPredFactory )

bool operator! ( EConcertActivityFilterFlags E )

EConcertActivityFilterFlags operator& ( EConcertActivityFilterFlags Lhs, EConcertActivityFilterFlags Rhs )

EConcertActivityFilterFlags & operator&= ( EConcertActivityFilterFlags& Lhs, EConcertActivityFilterFlags Rhs )

EConcertActivityFilterFlags operator^ ( EConcertActivityFilterFlags Lhs, EConcertActivityFilterFlags Rhs )

EConcertActivityFilterFlags & operator^= ( EConcertActivityFilterFlags& Lhs, EConcertActivityFilterFlags Rhs )

EConcertActivityFilterFlags operator| ( EConcertActivityFilterFlags Lhs, EConcertActivityFilterFlags Rhs )

EConcertActivityFilterFlags & operator|= ( EConcertActivityFilterFlags& Lhs, EConcertActivityFilterFlags Rhs )

EConcertActivityFilterFlags operator~ ( EConcertActivityFilterFlags E )

virtual UE::ConcertSharedSlate::~IPropertySelectionSourceModel()

FActivityColumn UE::ConcertSharedSlate::ActivityColumn::AvatarColor()

FActivityColumn UE::ConcertSharedSlate::ActivityColumn::ClientName()

FActivityColumn UE::ConcertSharedSlate::ActivityColumn::DateTime()

FActivityColumn UE::ConcertSharedSlate::ActivityColumn::Operation()

FActivityColumn UE::ConcertSharedSlate::ActivityColumn::Package()

FActivityColumn UE::ConcertSharedSlate::ActivityColumn::Summary()

FText UE::ConcertSharedSlate::EvaluateGetClientParenthesesContent ( const FGetClientParenthesesContent& Getter, const FGuid& ClientId )

UE::ConcertSharedSlate::template TReplicationColumnEntry< TListItemType > UE::ConcertSharedSlate::MakeCheckboxColumn ( FName ColumnId, TCheckboxColumnDelegates< TListItemType > Delegates, FText DefaultLabel, const int32 Priority, const float ColumnWidth )

bool UE::ConcertSharedSlate::operator! ( EItemPickerFlags E )

bool UE::ConcertSharedSlate::operator! ( EChildRelationshipFlags E )

EItemPickerFlags UE::ConcertSharedSlate::operator& ( EItemPickerFlags Lhs, EItemPickerFlags Rhs )

EChildRelationshipFlags UE::ConcertSharedSlate::operator& ( EChildRelationshipFlags Lhs, EChildRelationshipFlags Rhs )

EItemPickerFlags & UE::ConcertSharedSlate::operator&= ( EItemPickerFlags& Lhs, EItemPickerFlags Rhs )

EChildRelationshipFlags & UE::ConcertSharedSlate::operator&= ( EChildRelationshipFlags& Lhs, EChildRelationshipFlags Rhs )

EItemPickerFlags UE::ConcertSharedSlate::operator^ ( EItemPickerFlags Lhs, EItemPickerFlags Rhs )

EChildRelationshipFlags UE::ConcertSharedSlate::operator^ ( EChildRelationshipFlags Lhs, EChildRelationshipFlags Rhs )

EItemPickerFlags & UE::ConcertSharedSlate::operator^= ( EItemPickerFlags& Lhs, EItemPickerFlags Rhs )

EChildRelationshipFlags & UE::ConcertSharedSlate::operator^= ( EChildRelationshipFlags& Lhs, EChildRelationshipFlags Rhs )

EItemPickerFlags UE::ConcertSharedSlate::operator| ( EItemPickerFlags Lhs, EItemPickerFlags Rhs )

EChildRelationshipFlags UE::ConcertSharedSlate::operator| ( EChildRelationshipFlags Lhs, EChildRelationshipFlags Rhs )

EItemPickerFlags & UE::ConcertSharedSlate::operator|= ( EItemPickerFlags& Lhs, EItemPickerFlags Rhs )

EChildRelationshipFlags & UE::ConcertSharedSlate::operator|= ( EChildRelationshipFlags& Lhs, EChildRelationshipFlags Rhs )

EItemPickerFlags UE::ConcertSharedSlate::operator~ ( EItemPickerFlags E )

EChildRelationshipFlags UE::ConcertSharedSlate::operator~ ( EChildRelationshipFlags E )

bool UE::ConcertSharedSlate::ReplicationColumns::TopLevel::operator! ( ENumPropertiesFlags E )

ENumPropertiesFlags UE::ConcertSharedSlate::ReplicationColumns::TopLevel::operator& ( ENumPropertiesFlags Lhs, ENumPropertiesFlags Rhs )

ENumPropertiesFlags & UE::ConcertSharedSlate::ReplicationColumns::TopLevel::operator&= ( ENumPropertiesFlags& Lhs, ENumPropertiesFlags Rhs )

ENumPropertiesFlags UE::ConcertSharedSlate::ReplicationColumns::TopLevel::operator^ ( ENumPropertiesFlags Lhs, ENumPropertiesFlags Rhs )

ENumPropertiesFlags & UE::ConcertSharedSlate::ReplicationColumns::TopLevel::operator^= ( ENumPropertiesFlags& Lhs, ENumPropertiesFlags Rhs )

ENumPropertiesFlags UE::ConcertSharedSlate::ReplicationColumns::TopLevel::operator| ( ENumPropertiesFlags Lhs, ENumPropertiesFlags Rhs )

ENumPropertiesFlags & UE::ConcertSharedSlate::ReplicationColumns::TopLevel::operator|= ( ENumPropertiesFlags& Lhs, ENumPropertiesFlags Rhs )

ENumPropertiesFlags UE::ConcertSharedSlate::ReplicationColumns::TopLevel::operator~ ( ENumPropertiesFlags E )

bool UE::ConcertSharedSlate::SortLocalClientParenthesesFirstThenThenAlphabetical ( const FConcertSessionClientInfo& Left, const FConcertSessionClientInfo& Right, const FGetClientParenthesesContent& GetClientParenthesesContent )

bool UE::ConcertSharedSlate::SortSpecifiedParenthesesFirstThenThenAlphabetical ( const FConcertSessionClientInfo& Left, const FConcertSessionClientInfo& Right, const FGetClientParenthesesContent& GetClientParenthesesContent, const FText& ParenthesesContentToPlaceFirst )

static const FName ConcertBrowserUtils::ActiveSessionsCheckBoxMenuName ( TEXT("ActiveSessions") )

static const FName ConcertBrowserUtils::ArchivedSessionsCheckBoxMenuName ( TEXT("ArchivedSessions") )

static const FName ConcertBrowserUtils::DefaultServerCheckBoxMenuName ( TEXT("DefaultServer") )

static const FName ConcertBrowserUtils::IconColumnFontName ( TEXT("FontAwesome.9") )

static const FName ConcertBrowserUtils::LastModifiedCheckBoxMenuName ( TEXT("LastModified") )

static const FName ConcertBrowserUtils::LastModifiedColName ( TEXT("LastModified") )

static const FName ConcertBrowserUtils::ProjectColName ( TEXT("Project") )

static const FName ConcertBrowserUtils::ServerColName ( TEXT("Server") )

static const FName ConcertBrowserUtils::SessionColName ( TEXT("Session") )

static const FName ConcertBrowserUtils::VersionColName ( TEXT("Version") )

static TSharedRef< SComboButton > ConcertFrontendUtils::CreateViewOptionsComboButton ( FOnGetContent GetMenuContentDelegate )

static FText ConcertFrontendUtils::FormatRelativeTime ( const FDateTime& EventTime, const FDateTime* CurrTime )

static FText ConcertFrontendUtils::FormatTime ( const FDateTime& Time, ETimeFormat TimeFormat, const FDateTime* CurrTime )



---

## ConcertSyncClient

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ConcertSyncClient

**Contents:**
- ConcertSyncClient
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

bool operator! ( EConcertDataStoreChangeNotificationOptions E )

EConcertDataStoreChangeNotificationOptions operator& ( EConcertDataStoreChangeNotificationOptions Lhs, EConcertDataStoreChangeNotificationOptions Rhs )

EConcertDataStoreChangeNotificationOptions & operator&= ( EConcertDataStoreChangeNotificationOptions& Lhs, EConcertDataStoreChangeNotificationOptions Rhs )

EConcertDataStoreChangeNotificationOptions operator^ ( EConcertDataStoreChangeNotificationOptions Lhs, EConcertDataStoreChangeNotificationOptions Rhs )

EConcertDataStoreChangeNotificationOptions & operator^= ( EConcertDataStoreChangeNotificationOptions& Lhs, EConcertDataStoreChangeNotificationOptions Rhs )

EConcertDataStoreChangeNotificationOptions operator| ( EConcertDataStoreChangeNotificationOptions Lhs, EConcertDataStoreChangeNotificationOptions Rhs )

EConcertDataStoreChangeNotificationOptions & operator|= ( EConcertDataStoreChangeNotificationOptions& Lhs, EConcertDataStoreChangeNotificationOptions Rhs )

EConcertDataStoreChangeNotificationOptions operator~ ( EConcertDataStoreChangeNotificationOptions E )



---

## ConcertSyncCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ConcertSyncCore

**Contents:**
- ConcertSyncCore
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

void ActivitySummaryUtil::DebugPrintExportedObject ( const FConcertExportedObject& Object )

void ActivitySummaryUtil::DebugPrintExportedObject ( const FString& Pathname, const FConcertExportedObject* Objects )

void ActivitySummaryUtil::DebugPrintExportedObjects ( const FString::ElementType* Title, const TArray< TPair< const FString*, const FConcertExportedObject* > >& Objects )

void ActivitySummaryUtil::DebugPrintExportedObjects ( const FString::ElementType* Title, const TArray< TPair< FString, const FConcertExportedObject* > >& Objects )

FName ActivitySummaryUtil::GetObjectDisplayName ( const FString& ObjectPathName )

FName ActivitySummaryUtil::GetObjectDisplayName ( const FString& OuterPathName, const FName& ObjectName )

FText ActivitySummaryUtil::ToRichTextBold ( const FText& InArgs, bool bToRichText )

FText ActivitySummaryUtil::ToRichTextBold ( const FString& InArgs, bool bToRichText )

FText ActivitySummaryUtil::ToRichTextBold ( const FName& InArgs, bool bToRichText )

bool ConcertSyncSessionDatabaseFilterUtil::PackageEventPassesFilter ( const int64 InPackageEventId, const FConcertSessionFilter& InSessionFilter, const FConcertSyncSessionDatabase& InDatabase )

bool ConcertSyncSessionDatabaseFilterUtil::TransactionEventPassesFilter ( const int64 InTransactionEventId, const FConcertSessionFilter& InSessionFilter, const FConcertSyncSessionDatabase& InDatabase )

uint32 GetTypeHash ( const FConcertObjectId& ConcertObjectId )

uint32 GetTypeHash ( const FConcertPropertyChain& Chain )

uint32 GetTypeHash ( const FConcertObjectInStreamID& StreamObject )

uint32 GetTypeHash ( const FConcertReplicatedObjectId& StreamObject )

bool operator! ( EConcertSyncSessionFlags E )

bool operator! ( EConcertSyncActivityFlags E )

bool operator! ( EConcertReplicationChangeFrequencyFlags E )

bool operator! ( EConcertQueryClientStreamFlags E )

bool operator! ( EConcertReplicationMuteRequestFlags E )

bool operator! ( EConcertReplicationPutStateFlags E )

bool operator! ( EConcertReplicationRestoreContentFlags E )

EConcertSyncSessionFlags operator& ( EConcertSyncSessionFlags Lhs, EConcertSyncSessionFlags Rhs )

EConcertSyncActivityFlags operator& ( EConcertSyncActivityFlags Lhs, EConcertSyncActivityFlags Rhs )

EConcertReplicationChangeFrequencyFlags operator& ( EConcertReplicationChangeFrequencyFlags Lhs, EConcertReplicationChangeFrequencyFlags Rhs )

EConcertQueryClientStreamFlags operator& ( EConcertQueryClientStreamFlags Lhs, EConcertQueryClientStreamFlags Rhs )

EConcertReplicationMuteRequestFlags operator& ( EConcertReplicationMuteRequestFlags Lhs, EConcertReplicationMuteRequestFlags Rhs )

EConcertReplicationPutStateFlags operator& ( EConcertReplicationPutStateFlags Lhs, EConcertReplicationPutStateFlags Rhs )

EConcertReplicationRestoreContentFlags operator& ( EConcertReplicationRestoreContentFlags Lhs, EConcertReplicationRestoreContentFlags Rhs )

EConcertSyncSessionFlags & operator&= ( EConcertSyncSessionFlags& Lhs, EConcertSyncSessionFlags Rhs )

EConcertSyncActivityFlags & operator&= ( EConcertSyncActivityFlags& Lhs, EConcertSyncActivityFlags Rhs )

EConcertReplicationChangeFrequencyFlags & operator&= ( EConcertReplicationChangeFrequencyFlags& Lhs, EConcertReplicationChangeFrequencyFlags Rhs )

EConcertQueryClientStreamFlags & operator&= ( EConcertQueryClientStreamFlags& Lhs, EConcertQueryClientStreamFlags Rhs )

EConcertReplicationMuteRequestFlags & operator&= ( EConcertReplicationMuteRequestFlags& Lhs, EConcertReplicationMuteRequestFlags Rhs )

EConcertReplicationPutStateFlags & operator&= ( EConcertReplicationPutStateFlags& Lhs, EConcertReplicationPutStateFlags Rhs )

EConcertReplicationRestoreContentFlags & operator&= ( EConcertReplicationRestoreContentFlags& Lhs, EConcertReplicationRestoreContentFlags Rhs )

EConcertSyncSessionFlags operator^ ( EConcertSyncSessionFlags Lhs, EConcertSyncSessionFlags Rhs )

EConcertSyncActivityFlags operator^ ( EConcertSyncActivityFlags Lhs, EConcertSyncActivityFlags Rhs )

EConcertReplicationChangeFrequencyFlags operator^ ( EConcertReplicationChangeFrequencyFlags Lhs, EConcertReplicationChangeFrequencyFlags Rhs )

EConcertQueryClientStreamFlags operator^ ( EConcertQueryClientStreamFlags Lhs, EConcertQueryClientStreamFlags Rhs )

EConcertReplicationMuteRequestFlags operator^ ( EConcertReplicationMuteRequestFlags Lhs, EConcertReplicationMuteRequestFlags Rhs )

EConcertReplicationPutStateFlags operator^ ( EConcertReplicationPutStateFlags Lhs, EConcertReplicationPutStateFlags Rhs )

EConcertReplicationRestoreContentFlags operator^ ( EConcertReplicationRestoreContentFlags Lhs, EConcertReplicationRestoreContentFlags Rhs )

EConcertSyncSessionFlags & operator^= ( EConcertSyncSessionFlags& Lhs, EConcertSyncSessionFlags Rhs )

EConcertSyncActivityFlags & operator^= ( EConcertSyncActivityFlags& Lhs, EConcertSyncActivityFlags Rhs )

EConcertReplicationChangeFrequencyFlags & operator^= ( EConcertReplicationChangeFrequencyFlags& Lhs, EConcertReplicationChangeFrequencyFlags Rhs )

EConcertQueryClientStreamFlags & operator^= ( EConcertQueryClientStreamFlags& Lhs, EConcertQueryClientStreamFlags Rhs )

EConcertReplicationMuteRequestFlags & operator^= ( EConcertReplicationMuteRequestFlags& Lhs, EConcertReplicationMuteRequestFlags Rhs )

EConcertReplicationPutStateFlags & operator^= ( EConcertReplicationPutStateFlags& Lhs, EConcertReplicationPutStateFlags Rhs )

EConcertReplicationRestoreContentFlags & operator^= ( EConcertReplicationRestoreContentFlags& Lhs, EConcertReplicationRestoreContentFlags Rhs )

EConcertSyncSessionFlags operator| ( EConcertSyncSessionFlags Lhs, EConcertSyncSessionFlags Rhs )

EConcertSyncActivityFlags operator| ( EConcertSyncActivityFlags Lhs, EConcertSyncActivityFlags Rhs )

EConcertReplicationChangeFrequencyFlags operator| ( EConcertReplicationChangeFrequencyFlags Lhs, EConcertReplicationChangeFrequencyFlags Rhs )

EConcertQueryClientStreamFlags operator| ( EConcertQueryClientStreamFlags Lhs, EConcertQueryClientStreamFlags Rhs )

EConcertReplicationMuteRequestFlags operator| ( EConcertReplicationMuteRequestFlags Lhs, EConcertReplicationMuteRequestFlags Rhs )

EConcertReplicationPutStateFlags operator| ( EConcertReplicationPutStateFlags Lhs, EConcertReplicationPutStateFlags Rhs )

EConcertReplicationRestoreContentFlags operator| ( EConcertReplicationRestoreContentFlags Lhs, EConcertReplicationRestoreContentFlags Rhs )

EConcertSyncSessionFlags & operator|= ( EConcertSyncSessionFlags& Lhs, EConcertSyncSessionFlags Rhs )

EConcertSyncActivityFlags & operator|= ( EConcertSyncActivityFlags& Lhs, EConcertSyncActivityFlags Rhs )

EConcertReplicationChangeFrequencyFlags & operator|= ( EConcertReplicationChangeFrequencyFlags& Lhs, EConcertReplicationChangeFrequencyFlags Rhs )

EConcertQueryClientStreamFlags & operator|= ( EConcertQueryClientStreamFlags& Lhs, EConcertQueryClientStreamFlags Rhs )

EConcertReplicationMuteRequestFlags & operator|= ( EConcertReplicationMuteRequestFlags& Lhs, EConcertReplicationMuteRequestFlags Rhs )

EConcertReplicationPutStateFlags & operator|= ( EConcertReplicationPutStateFlags& Lhs, EConcertReplicationPutStateFlags Rhs )

EConcertReplicationRestoreContentFlags & operator|= ( EConcertReplicationRestoreContentFlags& Lhs, EConcertReplicationRestoreContentFlags Rhs )

EConcertSyncSessionFlags operator~ ( EConcertSyncSessionFlags E )

EConcertSyncActivityFlags operator~ ( EConcertSyncActivityFlags E )

EConcertReplicationChangeFrequencyFlags operator~ ( EConcertReplicationChangeFrequencyFlags E )

EConcertQueryClientStreamFlags operator~ ( EConcertQueryClientStreamFlags E )

EConcertReplicationMuteRequestFlags operator~ ( EConcertReplicationMuteRequestFlags E )

EConcertReplicationPutStateFlags operator~ ( EConcertReplicationPutStateFlags E )

EConcertReplicationRestoreContentFlags operator~ ( EConcertReplicationRestoreContentFlags E )

bool operator== ( const FConcertObjectId& A, const FConcertObjectId& B )

bool UE::ConcertSyncCore::AffectSubobjects ( EConcertReplicationMuteOption Option )

void UE::ConcertSyncCore::AppendSyncControl ( FConcertReplication_ChangeSyncControl& SyncControlToUpdate, const FConcertReplication_ChangeSyncControl& AppendedSyncControl, EAppendSyncControlFlags Flags )

FActivityDependencyGraph UE::ConcertSyncCore::BuildDependencyGraphFrom ( const FConcertSyncSessionDatabase& SessionDatabase )

uint32 UE::ConcertSyncCore::ComputeHashForPropertyChainContent ( const TArray< FName >& PropertyChain )

const FConcertObjectReplicationSettings * UE::ConcertSyncCore::FindObjectFrequency ( const TConstArrayView< FConcertReplicationStream > Streams, const FConcertObjectInStreamID& ObjectId )

FConcertObjectReplicationSettings * UE::ConcertSyncCore::FindObjectFrequencyEditable ( const TArrayView< FConcertReplicationStream > Streams, const FConcertObjectInStreamID& ObjectId )

const FConcertReplicatedObjectInfo * UE::ConcertSyncCore::FindObjectInfo ( const TConstArrayView< FConcertReplicationStream > Streams, const FConcertObjectInStreamID& ObjectId )

const FConcertReplicatedObjectInfo * UE::ConcertSyncCore::FindObjectInfo ( const FConcertReplicationStream& Stream, const FSoftObjectPath& ObjectPath )

FConcertReplicatedObjectInfo * UE::ConcertSyncCore::FindObjectInfoEditable ( const TArrayView< FConcertReplicationStream > Streams, const FConcertObjectInStreamID& ObjectId )

FConcertReplicatedObjectInfo * UE::ConcertSyncCore::FindObjectInfoEditable ( FConcertReplicationStream& Stream, const FSoftObjectPath& ObjectPath )

const FConcertReplicationStream * UE::ConcertSyncCore::FindStream ( const TConstArrayView< FConcertReplicationStream > Streams, const FGuid& StreamId )

FConcertReplicationStream * UE::ConcertSyncCore::FindStreamEditable ( const TArrayView< FConcertReplicationStream > Streams, const FGuid& StreamId )

FConcertReplicationRemappingData UE::ConcertSyncCore::GenerateRemappingData ( const FConcertObjectReplicationMap& Origin )

void UE::ConcertSyncCore::GenerateRemappingData ( const FConcertObjectReplicationMap& Origin, FConcertReplicationRemappingData& Result )

FConcertReplicationRemappingData UE::ConcertSyncCore::GenerateRemappingData ( const FConcertObjectReplicationMap& Origin, TGetObjectLabel&& GetLabelFunc, TGetObjectClass&& GetClassFunc )

void UE::ConcertSyncCore::GenerateRemappingData ( const FConcertObjectReplicationMap& Origin, TGetObjectLabel&& GetLabelFunc, TGetObjectClass&& GetClassFunc, FConcertReplicationRemappingData& Result )

TOptional< FSoftObjectPath > UE::ConcertSyncCore::GetActorPathIn ( const FSoftObjectPath& Path )

TOptional< FSoftObjectPath > UE::ConcertSyncCore::GetOuterPath ( const FSoftObjectPath& ObjectPath )

FString UE::ConcertSyncCore::GetReplicationActivityPayloadTypePathName ( EConcertSyncReplicationActivityType Type )

FString UE::ConcertSyncCore::Graphviz::ExportToGraphviz ( const FActivityDependencyGraph& Graph, const FConcertSyncSessionDatabase& SessionDatabase, ENodeTitleFlags NodeTitleFlags )

FString UE::ConcertSyncCore::Graphviz::ExportToGraphviz ( const FActivityDependencyGraph& Graph, FMakeNodeTitle MakeNodeTitleFunc, FGetNodeStyle GetNodeStyleFunc, FGetEdgeStyle GetEdgeStyleFunc )

void UE::ConcertSyncCore::Graphviz::GetEdgeStyle ( FGraphStringBuilder& WriteTo, const FActivityDependencyEdge& ToStringify )

void UE::ConcertSyncCore::Graphviz::GetNodeStyle ( FGraphStringBuilder& WriteTo, FActivityNodeID ToStringify, const FActivityDependencyGraph& Graph, const FConcertSyncSessionDatabase& SessionDatabase )

void UE::ConcertSyncCore::Graphviz::MakeNodeTitle ( FGraphStringBuilder& WriteTo, FActivityNodeID ToStringify, const FActivityDependencyGraph& Graph, const FConcertSyncSessionDatabase& SessionDatabase, ENodeTitleFlags NodeTitleFlags )

bool UE::ConcertSyncCore::Graphviz::operator! ( ENodeTitleFlags E )

ENodeTitleFlags UE::ConcertSyncCore::Graphviz::operator& ( ENodeTitleFlags Lhs, ENodeTitleFlags Rhs )

ENodeTitleFlags & UE::ConcertSyncCore::Graphviz::operator&= ( ENodeTitleFlags& Lhs, ENodeTitleFlags Rhs )

ENodeTitleFlags UE::ConcertSyncCore::Graphviz::operator^ ( ENodeTitleFlags Lhs, ENodeTitleFlags Rhs )

ENodeTitleFlags & UE::ConcertSyncCore::Graphviz::operator^= ( ENodeTitleFlags& Lhs, ENodeTitleFlags Rhs )

ENodeTitleFlags UE::ConcertSyncCore::Graphviz::operator| ( ENodeTitleFlags Lhs, ENodeTitleFlags Rhs )

ENodeTitleFlags & UE::ConcertSyncCore::Graphviz::operator|= ( ENodeTitleFlags& Lhs, ENodeTitleFlags Rhs )

ENodeTitleFlags UE::ConcertSyncCore::Graphviz::operator~ ( ENodeTitleFlags E )

bool UE::ConcertSyncCore::IsObjectOrChildReferenced ( const TConstArrayView< FConcertReplicationStream > Streams, const FSoftObjectPath& ObjectPath )

FString UE::ConcertSyncCore::LexToString ( EActivityDependencyReason Reason )

FString UE::ConcertSyncCore::LexToString ( EConcertReplicationRestoreErrorCode ErrorCode )

bool UE::ConcertSyncCore::operator! ( EActivityNodeFlags E )

bool UE::ConcertSyncCore::operator! ( EReplicationStreamCloneFlags E )

bool UE::ConcertSyncCore::operator! ( EAppendSyncControlFlags E )

EActivityNodeFlags UE::ConcertSyncCore::operator& ( EActivityNodeFlags Lhs, EActivityNodeFlags Rhs )

EReplicationStreamCloneFlags UE::ConcertSyncCore::operator& ( EReplicationStreamCloneFlags Lhs, EReplicationStreamCloneFlags Rhs )

EAppendSyncControlFlags UE::ConcertSyncCore::operator& ( EAppendSyncControlFlags Lhs, EAppendSyncControlFlags Rhs )

EActivityNodeFlags & UE::ConcertSyncCore::operator&= ( EActivityNodeFlags& Lhs, EActivityNodeFlags Rhs )

EReplicationStreamCloneFlags & UE::ConcertSyncCore::operator&= ( EReplicationStreamCloneFlags& Lhs, EReplicationStreamCloneFlags Rhs )

EAppendSyncControlFlags & UE::ConcertSyncCore::operator&= ( EAppendSyncControlFlags& Lhs, EAppendSyncControlFlags Rhs )

EActivityNodeFlags UE::ConcertSyncCore::operator^ ( EActivityNodeFlags Lhs, EActivityNodeFlags Rhs )

EReplicationStreamCloneFlags UE::ConcertSyncCore::operator^ ( EReplicationStreamCloneFlags Lhs, EReplicationStreamCloneFlags Rhs )

EAppendSyncControlFlags UE::ConcertSyncCore::operator^ ( EAppendSyncControlFlags Lhs, EAppendSyncControlFlags Rhs )

EActivityNodeFlags & UE::ConcertSyncCore::operator^= ( EActivityNodeFlags& Lhs, EActivityNodeFlags Rhs )

EReplicationStreamCloneFlags & UE::ConcertSyncCore::operator^= ( EReplicationStreamCloneFlags& Lhs, EReplicationStreamCloneFlags Rhs )

EAppendSyncControlFlags & UE::ConcertSyncCore::operator^= ( EAppendSyncControlFlags& Lhs, EAppendSyncControlFlags Rhs )

EActivityNodeFlags UE::ConcertSyncCore::operator| ( EActivityNodeFlags Lhs, EActivityNodeFlags Rhs )

EReplicationStreamCloneFlags UE::ConcertSyncCore::operator| ( EReplicationStreamCloneFlags Lhs, EReplicationStreamCloneFlags Rhs )

EAppendSyncControlFlags UE::ConcertSyncCore::operator| ( EAppendSyncControlFlags Lhs, EAppendSyncControlFlags Rhs )

EActivityNodeFlags & UE::ConcertSyncCore::operator|= ( EActivityNodeFlags& Lhs, EActivityNodeFlags Rhs )

EReplicationStreamCloneFlags & UE::ConcertSyncCore::operator|= ( EReplicationStreamCloneFlags& Lhs, EReplicationStreamCloneFlags Rhs )

EAppendSyncControlFlags & UE::ConcertSyncCore::operator|= ( EAppendSyncControlFlags& Lhs, EAppendSyncControlFlags Rhs )

EActivityNodeFlags UE::ConcertSyncCore::operator~ ( EActivityNodeFlags E )

EReplicationStreamCloneFlags UE::ConcertSyncCore::operator~ ( EReplicationStreamCloneFlags E )

EAppendSyncControlFlags UE::ConcertSyncCore::operator~ ( EAppendSyncControlFlags E )

TMap< FString, TArray< FSoftObjectPtr > > UE::ConcertSyncCore::Private::CacheByActorLabel ( const UWorld& World )

TOptional< FString > UE::ConcertSyncCore::Private::GetActorLabel ( const FSoftObjectPtr& Object )

FSoftClassPath UE::ConcertSyncCore::Private::GetClassPath ( const FSoftObjectPtr& Object )

FConcertObjectReplicationMap UE::ConcertSyncCore::RemapReplicationMap ( const FConcertObjectReplicationMap& Origin, const FConcertReplicationRemappingData& RemappingData, const UWorld& TargetWorld )

void UE::ConcertSyncCore::RemapReplicationMap ( const FConcertObjectReplicationMap& Origin, const FConcertReplicationRemappingData& RemappingData, const UWorld& TargetWorld, TProcessRemapping&& ProcessRemapping )

void UE::ConcertSyncCore::RemapReplicationMap ( const FConcertObjectReplicationMap& Origin, const FConcertReplicationRemappingData& RemappingData, const UWorld& TargetWorld, FConcertObjectReplicationMap& OutTargetMap )

FConcertObjectReplicationMap UE::ConcertSyncCore::RemapReplicationMap ( const FConcertObjectReplicationMap& Origin, const FConcertReplicationRemappingData& RemappingData, TIsRemappingCompatible&& IsRemappingCompatibleFunc, TForEachObjectWithLabel&& ForEachObjectWithLabelFunc, TGetObjectLabel&& GetLabelFunc )

void UE::ConcertSyncCore::RemapReplicationMap ( const FConcertObjectReplicationMap& Origin, const FConcertReplicationRemappingData& RemappingData, TIsRemappingCompatible&& IsRemappingCompatibleFunc, TForEachObjectWithLabel&& ForEachObjectWithLabelFunc, TGetObjectLabel&& GetLabelFunc, TProcessRemapping&& ProcessRemapping )

void UE::ConcertSyncCore::RemapReplicationMap ( const FConcertObjectReplicationMap& Origin, const FConcertReplicationRemappingData& RemappingData, TIsRemappingCompatible&& IsRemappingCompatibleFunc, TForEachObjectWithLabel&& ForEachObjectWithLabelFunc, TGetObjectLabel&& GetLabelFunc, FConcertObjectReplicationMap& OutTargetMap )

FOnPackageSaved & UE::ConcertSyncCore::SyncDatabase::GetOnPackageSavedDelegate()

static FText UE::ConcertSyncCore::ActivitySummary::Private::CreateDisplayText_LeaveReplication ( const FConcertSyncReplicationActivitySummary& Summary, const bool bInUseRichText )

static FText UE::ConcertSyncCore::ActivitySummary::Private::CreateDisplayText_Mute ( const FConcertSyncReplicationActivitySummary& Summary, const bool bInUseRichText )

static FText UE::ConcertSyncCore::ActivitySummary::Private::CreateDisplayTextForUser_LeaveReplication ( const FConcertSyncReplicationActivitySummary& Summary, const FText InUserDisplayName, const bool InUseRichText )

static FText UE::ConcertSyncCore::ActivitySummary::Private::CreateDisplayTextForUser_Mute ( const FConcertSyncReplicationActivitySummary& Summary, const FText InUserDisplayName, const bool bInUseRichText )

static FText UE::ConcertSyncCore::ActivitySummary::Private::SelectText ( bool bMuted, bool bUnmuted, const FText& MutedOnly, const FText& UnmutedOnly, const FText& MutedAndUnmuted )

static void UE::ConcertSyncCore::Private::GenericRemapReplicationMap ( const FConcertObjectReplicationMap& Origin, const FConcertReplicationRemappingData& RemappingData, const UWorld& TargetWorld, TFinalArg&& Argument )



---

## ConcertSyncServer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ConcertSyncServer

**Contents:**
- ConcertSyncServer
- Navigation
- Structs
- Interfaces
- Typedefs
- Constants
- Functions
  - Public

int32 ConcertSyncServerLoop ( const TCHAR* CommandLine, const FConcertSyncServerLoopInitArgs& InitArgs )

int32 ConcertSyncServerLoop ( const TCHAR* CommandLine, const FConcertSyncServerLoopInitArgs& InitArgs )

void ShutdownConcertSyncServer ( const FString& ServiceFriendlyName )

void ShutdownConcertSyncServer ( const FString& ServiceFriendlyName )



---

## ConcertTakeRecorder

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ConcertTakeRecorder

**Contents:**
- ConcertTakeRecorder
- Navigation
- Classes



---

## ConcertTransport

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ConcertTransport

**Contents:**
- ConcertTransport
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

bool operator! ( EConcertMessageFlags E )

EConcertMessageFlags operator& ( EConcertMessageFlags Lhs, EConcertMessageFlags Rhs )

EConcertMessageFlags & operator&= ( EConcertMessageFlags& Lhs, EConcertMessageFlags Rhs )

EConcertMessageFlags operator^ ( EConcertMessageFlags Lhs, EConcertMessageFlags Rhs )

EConcertMessageFlags & operator^= ( EConcertMessageFlags& Lhs, EConcertMessageFlags Rhs )

EConcertMessageFlags operator| ( EConcertMessageFlags Lhs, EConcertMessageFlags Rhs )

EConcertMessageFlags & operator|= ( EConcertMessageFlags& Lhs, EConcertMessageFlags Rhs )

EConcertMessageFlags operator~ ( EConcertMessageFlags E )

bool UE::ConcertTrace::IsTracingReplication()

uint8 UE::ConcertTrace::ProtocolSuiteToInt ( EProtocolSuite Id )



---

## Concert

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Concert

**Contents:**
- Concert
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

FArchiveSession_WithSession & ConcertServerEvents::ArchiveSession_WithSession()

FArchiveSession_WithWorkingDir & ConcertServerEvents::ArchiveSession_WithWorkingDir()

FCopySession & ConcertServerEvents::CopySession()

FExportSession & ConcertServerEvents::ExportSession()

FOnArchivedSessionCreated & ConcertServerEvents::OnArchivedSessionCreated()

FOnArchivedSessionDestroyed & ConcertServerEvents::OnArchivedSessionDestroyed()

FOnArchivedSessionRenamed & ConcertServerEvents::OnArchivedSessionRenamed()

FOnLiveSessionCreated & ConcertServerEvents::OnLiveSessionCreated()

FOnLiveSessionDestroyed & ConcertServerEvents::OnLiveSessionDestroyed()

FOnLiveSessionRenamed & ConcertServerEvents::OnLiveSessionRenamed()

FRestoreSession & ConcertServerEvents::RestoreSession()

bool ConcertUtil::Copy ( FArchive& DstAr, FArchive& SrcAr, int64 Size )

IConcertTransportLoggerRef ConcertUtil::CreateLogger ( const FConcertEndpointContext& InOwnerContext, FLogListener LogListenerFunc )

bool ConcertUtil::DeleteDirectoryTree ( const TCHAR* InDirectoryToDelete, const TCHAR* InMoveToDirBeforeDelete )

void ConcertUtil::SetVerboseLogging ( bool bInState )

bool operator! ( EConcertServerFlags E )

bool operator! ( EConcertCompressionDetails E )

bool operator! ( EBatchSessionDeletionFlags E )

EConcertServerFlags operator& ( EConcertServerFlags Lhs, EConcertServerFlags Rhs )

EConcertCompressionDetails operator& ( EConcertCompressionDetails Lhs, EConcertCompressionDetails Rhs )

EBatchSessionDeletionFlags operator& ( EBatchSessionDeletionFlags Lhs, EBatchSessionDeletionFlags Rhs )

EConcertServerFlags & operator&= ( EConcertServerFlags& Lhs, EConcertServerFlags Rhs )

EConcertCompressionDetails & operator&= ( EConcertCompressionDetails& Lhs, EConcertCompressionDetails Rhs )

EBatchSessionDeletionFlags & operator&= ( EBatchSessionDeletionFlags& Lhs, EBatchSessionDeletionFlags Rhs )

EConcertServerFlags operator^ ( EConcertServerFlags Lhs, EConcertServerFlags Rhs )

EConcertCompressionDetails operator^ ( EConcertCompressionDetails Lhs, EConcertCompressionDetails Rhs )

EBatchSessionDeletionFlags operator^ ( EBatchSessionDeletionFlags Lhs, EBatchSessionDeletionFlags Rhs )

EConcertServerFlags & operator^= ( EConcertServerFlags& Lhs, EConcertServerFlags Rhs )

EConcertCompressionDetails & operator^= ( EConcertCompressionDetails& Lhs, EConcertCompressionDetails Rhs )

EBatchSessionDeletionFlags & operator^= ( EBatchSessionDeletionFlags& Lhs, EBatchSessionDeletionFlags Rhs )

EConcertServerFlags operator| ( EConcertServerFlags Lhs, EConcertServerFlags Rhs )

EConcertCompressionDetails operator| ( EConcertCompressionDetails Lhs, EConcertCompressionDetails Rhs )

EBatchSessionDeletionFlags operator| ( EBatchSessionDeletionFlags Lhs, EBatchSessionDeletionFlags Rhs )

EConcertServerFlags & operator|= ( EConcertServerFlags& Lhs, EConcertServerFlags Rhs )

EConcertCompressionDetails & operator|= ( EConcertCompressionDetails& Lhs, EConcertCompressionDetails Rhs )

EBatchSessionDeletionFlags & operator|= ( EBatchSessionDeletionFlags& Lhs, EBatchSessionDeletionFlags Rhs )

EConcertServerFlags operator~ ( EConcertServerFlags E )

EConcertCompressionDetails operator~ ( EConcertCompressionDetails E )

EBatchSessionDeletionFlags operator~ ( EBatchSessionDeletionFlags E )

bool UE::Concert::Compression::DataIsCompressed ( EConcertCompressionDetails InFormat )

bool UE::Concert::Compression::DataIsCompressedWithOodle ( EConcertCompressionDetails InFormat )

bool UE::Concert::Compression::DataIsUncompressed ( EConcertCompressionDetails InFormat )

FName UE::Concert::Compression::GetCompressionAlgorithm ()

FName UE::Concert::Compression::GetCompressionAlgorithm ( EConcertCompressionDetails InDetails )

EConcertCompressionDetails UE::Concert::Compression::GetCompressionDetails ( SizeType DataSize )

ECompressionFlags UE::Concert::Compression::GetCompressionFlags ()

EConcertCompressionDetails UE::Concert::Compression::GetCompressionFlags ( EConcertCompressionDetails InFormat )

EConcertCompressionDetails UE::Concert::Compression::GetCompressionFromNamedType ( FName NamedMethod, ECompressionFlags Flags )

ECompressionFlags UE::Concert::Compression::GetCoreCompressionFlags ( EConcertCompressionDetails InFormat )

bool UE::Concert::Compression::ShouldCompress ( SizeType DataSize )



---

## ConsoleVariablesEditorRuntime

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ConsoleVariablesEditorRuntime

**Contents:**
- ConsoleVariablesEditorRuntime
- Navigation
- Classes
- Structs
- Constants



---

## ConsoleVariablesEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ConsoleVariablesEditor

**Contents:**
- ConsoleVariablesEditor
- Navigation
- Classes
- Structs
- Enums
  - Public
- Constants



---

## ContentBrowserAliasDataSource

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ContentBrowserAliasDataSource

**Contents:**
- ContentBrowserAliasDataSource
- Navigation
- Classes
- Structs
- Typedefs



---

## ContentBrowserAssetDataSource

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ContentBrowserAssetDataSource

**Contents:**
- ContentBrowserAssetDataSource
- Navigation
- Classes
- Structs



---

## ContentBrowserClassDataSource

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ContentBrowserClassDataSource

**Contents:**
- ContentBrowserClassDataSource
- Navigation
- Classes
- Structs



---

## ContentBrowserFileDataSource

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ContentBrowserFileDataSource

**Contents:**
- ContentBrowserFileDataSource
- Navigation
- Classes
- Structs



---

## Content Browser

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/content-browser-in-unreal-engine

**Contents:**
- Content Browser
- Accessing the Content Browser
- Content Drawer
- Content Browser Topics

A tool you can use to view, manage, and work with all of the Assets in your project.

The Content Browser is the primary area of the Unreal Editor for creating, importing, organizing, viewing, and managing content Assets within your Unreal project. You can also use it to manage content folders and perform specific Asset operations, such as:

Browse to and interact with all of the Assets in your project.

Find Assets using a text filter, which you can optionally combine with more advanced filtering.

Organize Assets into private, local, or shared collections.

Identify Assets that might contain problems.

Migrate Assets between content folders or to a different project.

To learn more about each of these operations, refer to the Content Browser Topics section on this page.

There are three ways to open the Content Browser:

From the Window menu in the top menu bar.

From the Create menu on the Main Toolbar.

By clicking the Content Drawer button on the bottom toolbar of the editor. This opens a temporary Content Browser you can then dock to the editor window. To learn more, refer to the Content Drawer section on this page.

You can open up to four instances of the Content Browser at the same time. This is useful, for example, if you want to:

Have different Asset types filtered in different Content Browsers, such as one that just shows Static Meshes and another that just shows Materials.

Move Assets between different folders in your project.

By default, the Content Browser docks along the bottom of the Unreal Editor window. You can click and drag to re-dock it anywhere within the editor, or float it as its own window. You can also right-click the Content Browser tab and select Move to Sidebar, which will collapse the Content Browser to a clickable tab in the left-hand sidebar of the Unreal Editor window.

The Content Drawer is a special instance of the Content Browser with slightly different behavior. To open it, either:

Click the Content Drawer button on the bottom bar of the editor.

Use the Ctrl + Space Bar (Windows) or Cmd + Space Bar (macOS) keyboard shortcut.

The Content Drawer automatically minimizes when it loses focus (that is, when you click away from it). To keep it open, click the Dock in Layout button. This creates a new instance of the Content Browser, but you can still open a new Content Drawer.

The Dock in Layout button on the Content Drawer.

To learn more about working in the Content Browser, refer to the pages below.



---

## Content Browser Interface

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/content-browser-interface-in-unreal-engine

**Contents:**
- Content Browser Interface
- Navigation Bar
- Sources Panel
- Collections
- Filters Column
- Search Bar
- Asset View
- Settings Button

Describes the Content Browser interface and functionality.

The Content Browser is divided into the following areas:

The Navigation Bar contains controls for working with Assets, navigating back and forward between folder paths, and shows a breadcrumb trail path for the folder that is currently open.

These buttons have the following functionality:

To learn more about importing Assets to your project, refer to the Importing Assets Directly page.

The Sources panel contains a list of all folders inside your Unreal Engine project.

This hierarchical list shows all folders in your Unreal Engine project. It behaves the same as the folder tree in Windows Explorer or the Finder in macOS. To expand or collapse a folder, click the arrow next to its name.

You can exclude folders from the Asset Tree by prefixing the search text with a hyphen (-). For example, entering -anim in the Search box hides any folder whose name contains that string, such as Animation or Animator.

For more information about the Sources panel, refer to the Sources Panel Reference page.

The Collections panel displays a list of all the Collections you have access to.

For more information on Collections and their use, refer to the Filters and Collections page.

The Filters column contains all built-in and custom filters for the user that is currently logged in. Click a filter to enable or disable it.

For more information on working with filters, refer to the Filters and Collections page.

The Search bar provides a wide range of functionality for quickly locating Assets based on their name and type. The Asset View, which displays the contents of the folder you select in the Sources panel, updates dynamically based on the parameters you enter here.

Click this button to open the Filters menu, which you can use to customize the kinds of Assets that display in the Asset View.

For more information on working with filters, refer to the Filters and Collections page.

The Asset View shows all available Assets within the currently selected folder or Collection.

From the Asset View, you can:

Drag and drop Assets directly into the Level.

Create and import Assets from the context menu that opens when you right-click inside the Asset View.

This button opens the Settings menu, where you can adjust the following settings for the Content Browser:

View style (how Assets are displayed: Tiles, Lists, or Columns).

Content to include or exclude.

For more information, refer to the Content Browser Settings Reference page.



---

## Content Browser Settings Reference

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/content-browser-settings-in-unreal-engine

**Contents:**
- Content Browser Settings Reference
- View Type
  - Tiles
  - List
  - Columns
- Locking
- View
  - Content
- Search
  - Thumbnails

Adjust thumbnail display, Asset filtering, and other areas of the Content Browser.

The Settings button is located in the top-right corner of the Content Browser. Clicking it opens a menu where you can adjust various settings for the current instance of the Content Browser, such as:

View type (how Assets are displayed: Tiles, Lists, or Columns).

Content to include or exclude.

These settings affect how Assets in the Asset View are displayed. You can choose one of the following View Types:

The Tiles view lays out all Assets into a grid of tiles, like so:

The List view lays out all Assets into a list of thumbnails with names and file types, like so:

The Columns view lays out all Assets with a spreadsheet-like arrangement of properties, like so:

The details displayed change depending on the type of Asset. For example, Blueprint Assets display their Type and Parent Class, and Static Meshes display their vertices and triangles counts.

You can perform the following operations on each column:

Sort the Assets by the column's value in ascending or descending order by left-clicking the column name.

Hide a column by hovering over its name, then clicking the vertical ellipsis menu and selecting Hide Column.

Unhide columns from the Settings menu by selecting the Toggle Columns option and enabling the columns you want to display.

You can also export all of the Asset details as a .csv file. From the Settings menu, select the Export to CSV option. Note that this option only displays if the Asset Viewer is currently using the Columns view.

The Lock Content Browser option is a toggleable setting. If enabled, this instance of the Content Browser will ignore Find in Content Browser requests.

Use the View settings to toggle what displays in the Content Browser, as well as filtering behavior.

Disable this option to have the Content Browser show all Assets in the project in a single view.

Disable the Show Empty Folders sub-option to have the Content Browser show only folders that contain at least one Asset.

Enabling this option adds a new Favorites category at the top of the Sources panel. This category displays if you have added at least one folder or Asset to your Favorites.

To add a folder or Asset to your Favorites, right-click it, then select Add To Favorites from the context menu.

Toggle the following options to control whether or not certain types of Assets display in the Asset View.

Use the Search options to control what gets included or excluded from searches performed within the Content Browser:

Use the Thumbnail options to control how thumbnails are generated and displayed.

Choose from one of the five possible sizes for thumbnails that display in the Asset View:

If enabled, you can adjust the thumbnails of 3D Assets by left-clicking and dragging inside the thumbnail. When you are finished, click the Done Editing button to save your changes. To revert your changes, click the Undo button in the top-right corner of the thumbnail.

You must save your Asset to save the changes you made to its thumbnail.

You can adjust further settings that affect the Content Browser from the Editor Preferences (menu: Edit > Editor Preferences, then select the Content Browser section).



---

## ContextualAnimationEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ContextualAnimationEditor

**Contents:**
- ContextualAnimationEditor
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## ContextualAnimation

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ContextualAnimation

**Contents:**
- ContextualAnimation
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## ControlFlows

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ControlFlows

**Contents:**
- ControlFlows
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Constants
- Functions
  - Static

static bool UE::Private::OwningObjectIsValid ( TSharedRef< const FControlFlowContainerBase > InFlowContainer )



---

## ControlRigDeveloper

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ControlRigDeveloper

**Contents:**
- ControlRigDeveloper
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## ControlRigEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ControlRigEditor

**Contents:**
- ControlRigEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

FKeyHandle AddOrUpdateKey ( FMovieSceneControlRigSpaceChannel* Channel, UMovieSceneSection* SectionToKey, FFrameNumber Time, ISequencer& Sequencer, const FGuid& ObjectBindingID, FTrackInstancePropertyBindings* PropertyBindings )

bool CanCreateKeyEditor ( const FMovieSceneControlRigSpaceChannel* Channel )

TUniquePtr< FCurveModel > CreateCurveEditorModel ( const TMovieSceneChannelHandle< FMovieSceneControlRigSpaceChannel >& Channel, const UE::Sequencer::FCreateCurveEditorModelParams& Params )

TSharedRef< SWidget > CreateKeyEditor ( const TMovieSceneChannelHandle< FMovieSceneControlRigSpaceChannel >& Channel, const UE::Sequencer::FCreateKeyEditorParams& Params )

int32 DrawExtra ( FMovieSceneControlRigSpaceChannel* Channel, const UMovieSceneSection* Owner, const FSequencerChannelPaintArgs& PaintArgs, int32 LayerId )

void DrawKeys ( FMovieSceneControlRigSpaceChannel* Channel, TArrayView< const FKeyHandle > InKeyHandles, const UMovieSceneSection* InOwner, TArrayView< FKeyDrawParams > OutKeyDrawParams )

bool SupportsCurveEditorModels ( const TMovieSceneChannelHandle< FMovieSceneControlRigSpaceChannel >& Channel )

void UE::AIE::AddKeyToChannel ( ChannelType* Channel, EMovieSceneKeyInterpolation DefaultInterpolation, const FFrameNumber& FrameNumber, ValueType Value )

void UE::AIE::AssigneOrSetValue ( ChannelType* Channel, ValueType Value, const FFrameNumber& FrameNumber, EMovieSceneKeyInterpolation DefaultInterpolation )

void UE::AIE::SetCurrentKeys ( TArrayView< ChannelType* > Channels, int32 StartIndex, int32 EndIndex, EMovieSceneKeyInterpolation DefaultInterpolation, const FFrameNumber& FrameNumber )



---

## ControlRigPhysics

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ControlRigPhysics

**Contents:**
- ControlRigPhysics
- Navigation
- Classes
- Structs
- Enums
  - Public
- Variables
  - Public



---

## ControlRigSpline

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ControlRigSpline

**Contents:**
- ControlRigSpline
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## ControlRig

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ControlRig

**Contents:**
- ControlRig
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

bool ERigTransformType::IsCurrent ( const Type InTransformType )

bool ERigTransformType::IsGlobal ( const Type InTransformType )

bool ERigTransformType::IsInitial ( const Type InTransformType )

bool ERigTransformType::IsLocal ( const Type InTransformType )

Type ERigTransformType::MakeCurrent ( const Type InTransformType )

Type ERigTransformType::MakeGlobal ( const Type InTransformType )

Type ERigTransformType::MakeInitial ( const Type InTransformType )

Type ERigTransformType::MakeLocal ( const Type InTransformType )

ERigTransformType::Type ERigTransformType::SwapCurrentAndInitial ( const Type InTransformType )

Type ERigTransformType::SwapLocalAndGlobal ( const Type InTransformType )

bool EvaluateChannel ( const FMovieSceneControlRigSpaceChannel* InChannel, FFrameTime InTime, FMovieSceneControlRigSpaceBaseKey& OutValue )

Type FRigMathLibrary::Add ( const Type Argument0, const Type Argument1 )

Type FRigMathLibrary::Divide ( const Type Argument0, const Type Argument1 )

Type FRigMathLibrary::Multiply ( const Type Argument0, const Type Argument1 )

Type FRigMathLibrary::Subtract ( const Type Argument0, const Type Argument1 )

uint32 GetTypeHash ( const FRigHierarchyRecord& InRecord )

uint32 GetTypeHash ( const FInstructionRecord& InRecord )

bool operator! ( EControlRigContextChannelToKey E )

EControlRigContextChannelToKey operator& ( EControlRigContextChannelToKey Lhs, EControlRigContextChannelToKey Rhs )

EControlRigContextChannelToKey & operator&= ( EControlRigContextChannelToKey& Lhs, EControlRigContextChannelToKey Rhs )

EControlRigContextChannelToKey operator^ ( EControlRigContextChannelToKey Lhs, EControlRigContextChannelToKey Rhs )

EControlRigContextChannelToKey & operator^= ( EControlRigContextChannelToKey& Lhs, EControlRigContextChannelToKey Rhs )

EControlRigContextChannelToKey operator| ( EControlRigContextChannelToKey Lhs, EControlRigContextChannelToKey Rhs )

EControlRigContextChannelToKey & operator|= ( EControlRigContextChannelToKey& Lhs, EControlRigContextChannelToKey Rhs )

EControlRigContextChannelToKey operator~ ( EControlRigContextChannelToKey E )

T * RigUnit_AnimAttribute::GetAnimAttributeValue ( bool bAddIfNotFound, const FControlRigExecuteContext& Context, const FName& Name, const FName& BoneName, FName& CachedBoneName, int32& CachedBoneIndex )

FName UtilityHelpers::CreateUniqueName ( const FName& InBaseName, Predicate IsUnique )

FTransform UtilityHelpers::GetBaseTransformByMode ( ETransformSpaceMode TransformSpaceMode, Predicate TransformGetter, const FRigElementKey& ParentKey, const FRigElementKey& BaseKey, const FTransform& BaseTransform )

static uint32 FRigElementTypeHelper::Add ( uint32 InMasks, ERigElementType InType )

static bool FRigElementTypeHelper::DoesHave ( uint32 InMasks, ERigElementType InType )

static uint32 FRigElementTypeHelper::Remove ( uint32 InMasks, ERigElementType InType )

static uint32 FRigElementTypeHelper::ToMask ( ERigElementType InType )



---

## CPSLiveLinkDevice

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CPSLiveLinkDevice

**Contents:**
- CPSLiveLinkDevice
- Navigation
- Classes
- Structs



---

## CQTestEnhancedInput

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CQTestEnhancedInput

**Contents:**
- CQTestEnhancedInput
- Navigation
- Classes



---

## CryptoKeysOpenSSL

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CryptoKeysOpenSSL

**Contents:**
- CryptoKeysOpenSSL
- Navigation



---

## CryptoKeys

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CryptoKeys

**Contents:**
- CryptoKeys
- Navigation
- Classes
- Structs



---

## CsvMetrics

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CsvMetrics

**Contents:**
- CsvMetrics
- Navigation
- Classes



---

## CurveExpressionEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CurveExpressionEditor

**Contents:**
- CurveExpressionEditor
- Navigation
- Classes
- Interfaces



---

## CurveExpression

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CurveExpression

**Contents:**
- CurveExpression
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## CustomDetailsView

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CustomDetailsView

**Contents:**
- CustomDetailsView
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

bool operator! ( ECustomDetailsViewNodePropertyFlag E )

ECustomDetailsViewNodePropertyFlag operator& ( ECustomDetailsViewNodePropertyFlag Lhs, ECustomDetailsViewNodePropertyFlag Rhs )

ECustomDetailsViewNodePropertyFlag & operator&= ( ECustomDetailsViewNodePropertyFlag& Lhs, ECustomDetailsViewNodePropertyFlag Rhs )

ECustomDetailsViewNodePropertyFlag operator^ ( ECustomDetailsViewNodePropertyFlag Lhs, ECustomDetailsViewNodePropertyFlag Rhs )

ECustomDetailsViewNodePropertyFlag & operator^= ( ECustomDetailsViewNodePropertyFlag& Lhs, ECustomDetailsViewNodePropertyFlag Rhs )

ECustomDetailsViewNodePropertyFlag operator| ( ECustomDetailsViewNodePropertyFlag Lhs, ECustomDetailsViewNodePropertyFlag Rhs )

ECustomDetailsViewNodePropertyFlag & operator|= ( ECustomDetailsViewNodePropertyFlag& Lhs, ECustomDetailsViewNodePropertyFlag Rhs )

ECustomDetailsViewNodePropertyFlag operator~ ( ECustomDetailsViewNodePropertyFlag E )



---

## CustomizableObjectEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CustomizableObjectEditor

**Contents:**
- CustomizableObjectEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

FNodeType * GetCustomizableObjectExternalNode ( UCustomizableObject* Object, const FGuid& NodeGuid )



---

## CustomizableObjectPopulationEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CustomizableObjectPopulationEdit-

**Contents:**
- CustomizableObjectPopulationEditor
- Navigation
- Classes
- Interfaces
- Variables
  - Public



---

## CustomizableObjectPopulation

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CustomizableObjectPopulation

**Contents:**
- CustomizableObjectPopulation
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## CustomizableObject

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CustomizableObject

**Contents:**
- CustomizableObject
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

CUSTOMIZABLEOBJECT_APIUCustomizableObjectInstanceUsage * GetPlayerCustomizableObjectInstanceUsage ( const int32 SlotID, const UWorld* CurrentWorld, const int32 PlayerIndex )

uint32 GetTypeHash ( const FCustomizableObjectBoolParameterValue& Key )

uint32 GetTypeHash ( const FCustomizableObjectIntParameterValue& Key )

uint32 GetTypeHash ( const FCustomizableObjectFloatParameterValue& Key )

uint32 GetTypeHash ( const FCustomizableObjectTextureParameterValue& Key )

uint32 GetTypeHash ( const FCustomizableObjectSkeletalMeshParameterValue& Key )

uint32 GetTypeHash ( const FCustomizableObjectMaterialParameterValue& Key )

uint32 GetTypeHash ( const FCustomizableObjectVectorParameterValue& Key )

uint32 GetTypeHash ( const FCustomizableObjectTransformParameterValue& Key )

uint32 GetTypeHash ( const FCustomizableObjectProjector& Key )

uint32 GetTypeHash ( const FCustomizableObjectProjectorParameterValue& Key )

uint32 GetTypeHash ( const FMultilayerProjectorLayer& Key )

void PrintParticipatingPackagesDiff ( const TArray< FName >& OutOfDatePackages, const TArray< FName >& AddedPackages, const TArray< FName >& RemovedPackages, bool bReleaseVersion )



---

## CustomizableSequencerTracks

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CustomizableSequencerTracks

**Contents:**
- CustomizableSequencerTracks
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## Customizing Keyboard Shortcuts

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/customizing-keyboard-shortcuts-in-unreal-engine

**Contents:**
- Customizing Keyboard Shortcuts
- Creating a New Keyboard Shortcut
- Removing an Existing Keyboard Shortcut
- Importing and Exporting Keyboard Shortcuts

Change keyboard shortcuts for common commands in Unreal Engine and create new shortcuts to suit your workflows.

Keyboard shortcuts, also known as keybinds, are combinations of key presses on your keyboard that execute specific commands or actions. You can configure the shortcuts for common commands, as well as some tool-specific commands, to suit your workflow and personal preferences. To do this, open the Editor Preferences window: from the main menu, go to Edit > Editor Preferences, then select the Keyboard Shortcuts section.

The Keyboard Shortcuts editor in the Editor Preferences window.

Commands are grouped by functional area. Each command can have up to two keyboard shortcuts associated with it.

Click inside the text field for the command you want to bind to a keyboard shortcut.

Press the combination of keys you want to use to execute the command.

Unreal Engine will automatically save the new shortcut when you click anywhere outside the text field.

If the combination of keys you pressed is already bound to another command, you will see a warning.

If you want to remove the existing binding and assign the keyboard shortcut to the new command, click the Override button. If you want to keep the existing binding and cancel the new one, click anywhere outside the text field.

To remove an existing keyboard shortcut, click the Delete (X) button next to it.

You can migrate your custom keybinds between different installations of Unreal Engine by exporting them as an .ini file that you can then import into another UE installation. This is useful, for example, if you work on different computers, or if you rebuild or reinstall Unreal Engine often.

To save your custom keybinds as an .ini file, click the Export button. To import a set of custom keybinds from an .ini file, click the Import button. Both of these buttons are located at the top of the Keyboard Shortcuts editor.

Location of the Export and Import buttons.



---

## CustomMeshComponent

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/CustomMeshComponent

**Contents:**
- CustomMeshComponent
- Navigation
- Classes
- Structs
- Interfaces



---

## DatabaseSupport

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DatabaseSupport

**Contents:**
- DatabaseSupport
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## DataflowAssetTools

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataflowAssetTools

**Contents:**
- DataflowAssetTools
- Navigation
- Structs



---

## DataflowEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataflowEditor

**Contents:**
- DataflowEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

FName UE::Dataflow::CollectionSpreadSheetHelpers::GetArrayTypeString ( FManagedArrayCollection::EArrayType ArrayType )

void UE::Dataflow::Rendering::AddUvDynamicMeshComponent ( const T& Source, int32 UvIndex, FRenderableComponents& OutComponents )



---

## DataflowEnginePlugin

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataflowEnginePlugin

**Contents:**
- DataflowEnginePlugin
- Navigation
- Classes
- Structs
- Interfaces
- Functions
  - Public

UE_DATAFLOW_POLICY_DECLARE_TYPENAME ( TObjectPtr< UDynamicMesh > )



---

## DataflowNodes

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataflowNodes

**Contents:**
- DataflowNodes
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants



---

## DataIngestCoreEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataIngestCoreEditor

**Contents:**
- DataIngestCoreEditor
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## DataIngestCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataIngestCore

**Contents:**
- DataIngestCore
- Navigation
- Classes
- Structs
- Typedefs



---

## DataLinkDataTable

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataLinkDataTable

**Contents:**
- DataLinkDataTable
- Navigation
- Classes
- Functions
  - Public

const FLazyName UE::DataLinkDataTable::InputRow ( TEXT("InputRow") )



---

## DataLinkEdGraph

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataLinkEdGraph

**Contents:**
- DataLinkEdGraph
- Navigation
- Classes



---

## DataLinkEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataLinkEditor

**Contents:**
- DataLinkEditor
- Navigation
- Classes
- Interfaces
- Functions
  - Public

const FLazyName UE::DataLinkEditor::PreviewSectionName ( TEXT("Preview") )

const FLazyName UE::DataLinkEditor::PreviewToolbarName ( TEXT("DataLinkGraphAssetToolkit_PreviewToolbar") )



---

## DataLinkHttp

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataLinkHttp

**Contents:**
- DataLinkHttp
- Navigation
- Classes
- Structs
- Functions
  - Public

const FLazyName UE::DataLinkHttp::InputHttpSettings ( TEXT("InputHttpSettings") )



---

## DataLinkJson

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataLinkJson

**Contents:**
- DataLinkJson
- Navigation
- Classes
- Structs
- Functions
  - Public

TSharedPtr< FJsonValue > UE::DataLinkJson::FindJsonValue ( const TSharedRef< FJsonObject >& InJsonObject, const FString& InFieldName )

const FLazyName UE::DataLinkJson::InputJsonObject ( TEXT("InputJson") )

const FLazyName UE::DataLinkJson::InputMappingConfig ( TEXT("InputMapping") )

const FLazyName UE::DataLinkJson::InputString ( TEXT("InputString") )

const FLazyName UE::DataLinkJson::InputStruct ( TEXT("InputStruct") )



---

## DataLinkOAuth

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataLinkOAuth

**Contents:**
- DataLinkOAuth
- Navigation
- Classes
- Structs
- Functions
  - Public

const FLazyName UE::DataLinkOAuth::InputHttp ( TEXT("InputHttp") )

const FLazyName UE::DataLinkOAuth::InputOAuth ( TEXT("InputOAuth") )

TSharedPtr< FJsonObject > UE::DataLinkOAuth::ResponseStringToJsonObject ( FStringView InResponseString )



---

## DataLinkWebSocket

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataLinkWebSocket

**Contents:**
- DataLinkWebSocket
- Navigation
- Classes
- Structs



---

## DataLink

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataLink

**Contents:**
- DataLink
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

const FLazyName UE::DataLink::InputDefault ( TEXT("Input") )

const FLazyName UE::DataLink::InputReplaceSettings ( TEXT("InputReplaceSettings") )

const FLazyName UE::DataLink::OutputDefault ( TEXT("Output") )



---

## DataprepCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataprepCore

**Contents:**
- DataprepCore
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

virtual ~UDataprepActionAsset()

int32 AddStep ( TSubclassOf< UDataprepParameterizableObject > StepType )

int32 AddStep ( const UDataprepActionStep* ActionStep )

int32 AddStep ( const UDataprepParameterizableObject* StepObject )

int32 AddSteps ( const TArray< const UDataprepActionStep* >& ActionSteps )

void EnableStep ( int32 Index, bool bEnable )

void Execute ( const TArray< UObject* >& InObjects )

void ExecuteAction ( const TSharedPtr< FDataprepActionContext >& InActionsContext, UDataprepActionStep* SpecificStep, bool bSpecificStepOnly )

UDataprepActionAppearance * GetAppearance()

const TCHAR * GetLabel()

FOnStepAboutToBeRemoved & GetOnStepAboutToBeRemoved()

FOnStepsOrderChanged & GetOnStepsOrderChanged()

FOnStepWasEdited & GetOnStepWasEdited()

TWeakObjectPtr< UDataprepActionStep > GetStep ( int32 Index )

int32 GetStepsCount()

uint32 GetTypeHash ( const FDataprepPropertyLink& PropertyLink )

bool InsertStep ( const UDataprepActionStep* ActionStep, int32 Index )

bool InsertSteps ( const TArray< const UDataprepActionStep* >& ActionSteps, int32 Index )

bool IsStepEnabled ( int32 Index ) const

bool MoveStep ( int32 StepIndex, int32 DestinationIndex )

void NotifyDataprepSystemsOfRemoval()

virtual void PostTransacted ( const FTransactionObjectEvent& TransactionEvent )

bool RemoveStep ( int32 Index, bool bDiscardParametrization )

bool RemoveSteps ( const TArray< int32 >& Indices, bool bDiscardParametrization )

void SetLabel ( const TCHAR* InLabel )

bool SwapSteps ( int32 FirstIndex, int32 SecondIndex )

FOnStepWasEdited TBaseMulticastDelegate_TwoParams UDataprepActionAsset()



---

## DataprepEditorScriptingUtilities

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataprepEditorScriptingUtilities

**Contents:**
- DataprepEditorScriptingUtilities
- Navigation
- Classes
- Enums
  - Public



---

## DataprepEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataprepEditor

**Contents:**
- DataprepEditor
- Navigation
- Classes
- Interfaces
- Variables
  - Public



---

## DataprepLibraries

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataprepLibraries

**Contents:**
- DataprepLibraries
- Navigation
- Classes
- Interfaces



---

## DataRegistryEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataRegistryEditor

**Contents:**
- DataRegistryEditor
- Navigation
- Classes
- Typedefs



---

## DataRegistry

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataRegistry

**Contents:**
- DataRegistry
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Functions
  - Public

bool operator! ( EMetaDataRegistrySourceAssetUsage E )

EMetaDataRegistrySourceAssetUsage operator& ( EMetaDataRegistrySourceAssetUsage Lhs, EMetaDataRegistrySourceAssetUsage Rhs )

EMetaDataRegistrySourceAssetUsage & operator&= ( EMetaDataRegistrySourceAssetUsage& Lhs, EMetaDataRegistrySourceAssetUsage Rhs )

EMetaDataRegistrySourceAssetUsage operator^ ( EMetaDataRegistrySourceAssetUsage Lhs, EMetaDataRegistrySourceAssetUsage Rhs )

EMetaDataRegistrySourceAssetUsage & operator^= ( EMetaDataRegistrySourceAssetUsage& Lhs, EMetaDataRegistrySourceAssetUsage Rhs )

EMetaDataRegistrySourceAssetUsage operator| ( EMetaDataRegistrySourceAssetUsage Lhs, EMetaDataRegistrySourceAssetUsage Rhs )

EMetaDataRegistrySourceAssetUsage & operator|= ( EMetaDataRegistrySourceAssetUsage& Lhs, EMetaDataRegistrySourceAssetUsage Rhs )

EMetaDataRegistrySourceAssetUsage operator~ ( EMetaDataRegistrySourceAssetUsage E )



---

## DatasmithC4DTranslator

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DatasmithC4DTranslator

**Contents:**
- DatasmithC4DTranslator
- Navigation
- Interfaces



---

## DatasmithCADTranslator

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DatasmithCADTranslator

**Contents:**
- DatasmithCADTranslator
- Navigation
- Classes



---

## DatasmithContentEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DatasmithContentEditor

**Contents:**
- DatasmithContentEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## DatasmithContent

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DatasmithContent

**Contents:**
- DatasmithContent
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Variables
  - Public
- Functions

DataType * Datasmith::GetAdditionalData ( const FAssetData& SourceAssetData )

UAssetImportData * Datasmith::GetAssetImportData ( UObject* Asset )

TArray< DataType * > Datasmith::GetMultipleAdditionalData ( const FAssetData& SourceAssetData, int MaxCount )

DataType * Datasmith::MakeAdditionalData()



---

## DatasmithDeltaGenTranslator

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DatasmithDeltaGenTranslator

**Contents:**
- DatasmithDeltaGenTranslator
- Navigation
- Interfaces



---

## DatasmithDispatcher

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DatasmithDispatcher

**Contents:**
- DatasmithDispatcher
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## DatasmithExternalSource

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DatasmithExternalSource

**Contents:**
- DatasmithExternalSource
- Navigation
- Classes



---

## DatasmithFBXTranslator

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DatasmithFBXTranslator

**Contents:**
- DatasmithFBXTranslator
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

uint32 GetTypeHash ( const FMD5Hash& Hash )

bool operator! ( ENodeType E )

ENodeType operator& ( ENodeType Lhs, ENodeType Rhs )

ENodeType & operator&= ( ENodeType& Lhs, ENodeType Rhs )

ENodeType operator^ ( ENodeType Lhs, ENodeType Rhs )

ENodeType & operator^= ( ENodeType& Lhs, ENodeType Rhs )

ENodeType operator| ( ENodeType Lhs, ENodeType Rhs )

ENodeType & operator|= ( ENodeType& Lhs, ENodeType Rhs )

ENodeType operator~ ( ENodeType E )



---

## DatasmithImporter

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DatasmithImporter

**Contents:**
- DatasmithImporter
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## DatasmithInterchange

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DatasmithInterchange

**Contents:**
- DatasmithInterchange
- Navigation
- Classes
- Interfaces



---

## DatasmithMVRTranslator

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DatasmithMVRTranslator

**Contents:**
- DatasmithMVRTranslator
- Navigation
- Interfaces



---

## DatasmithNativeTranslator

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DatasmithNativeTranslator

**Contents:**
- DatasmithNativeTranslator
- Navigation
- Classes



---

## DatasmithOpenNurbsTranslator

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DatasmithOpenNurbsTranslator

**Contents:**
- DatasmithOpenNurbsTranslator
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## DatasmithPLMXMLTranslator

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DatasmithPLMXMLTranslator

**Contents:**
- DatasmithPLMXMLTranslator
- Navigation
- Interfaces



---

## DatasmithRuntime

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DatasmithRuntime

**Contents:**
- DatasmithRuntime
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## DatasmithTranslator

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DatasmithTranslator

**Contents:**
- DatasmithTranslator
- Navigation
- Classes
- Structs
- Interfaces
- Functions
  - Public

void Datasmith::Details::RegisterTranslatorImpl ( const FTranslatorRegisterInformation& Info )

void Datasmith::Details::UnregisterTranslatorImpl ( const FTranslatorRegisterInformation& Info )

bool DatasmithMeshHelper::IsTriangleDegenerated ( const FMeshDescription& Mesh, const FMeshTriangle& MeshTriangle )



---

## DatasmithVREDTranslator

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DatasmithVREDTranslator

**Contents:**
- DatasmithVREDTranslator
- Navigation
- Interfaces



---

## DatasmithWireTranslator

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DatasmithWireTranslator

**Contents:**
- DatasmithWireTranslator
- Navigation
- Structs
- Interfaces
- Typedefs



---

## Datasmith

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/datasmith-plugins-for-unreal-engine

**Contents:**
- Datasmith
- Getting Started
- Guides
- Software and File Type Interop Guides
- Reference

Datasmith gets your design data into Unreal quickly and easily.

Datasmith is a collection of tools and plugins that bring entire pre-constructed scenes and complex assets created in a variety of industry-standard design applications into Unreal Engine.

The following pages will help you understand how Datasmith works, what kind of results it produces in Unreal, and how to use it to start crafting real-time visualizations around your design content.

An overview of how Datasmith works, and what you should expect when you use it.

Importing Datasmith Content into Unreal Engine

How to use Datasmith to bring files that you create in supported 3D design applications into Unreal Engine.

Datasmith Exporter Plugin Release Notes

Information about the latest updates to the Datasmith Exporter plugins.

Datasmith Import Process

Contains details about specific issues in the way Datasmith imports scenes into Unreal, and next steps you can follow to work with the imported Assets in Unreal Engine.

Datasmith Reimport Workflow

Describes what happens when you reimport content that you brought into Unreal using Datasmith, and how you can take advantage of this iterative workflow.

Customizing the Datasmith Import Process

Describes how to import Datasmith and CAD files using Blueprint or Python, and how to change the way your scene is transformed into Unreal Assets and Actors.

Dataprep Import Customization

Make reusable recipes that import assets and prepare them for real-time rendering.

Using Datasmith Metadata

Get custom metadata about Assets into Unreal, and use Blueprint and Python scripting to work with that metadata in the Editor and at runtime.

Using Datasmith Direct Link

An overview of Datasmith Direct Link technology in Unreal Engine.

The Datasmith 3ds Max Exporter plugin brings content from Autodesk 3ds Max into the Unreal Editor.

How to import Datasmith scenes from Graphisoft Archicad into Unreal Engine.

Describes special considerations that apply only when you use Datasmith to bring scenes from Maxon Cinema 4D into the Unreal Editor.

Describes special considerations that apply when you use Datasmith to import scenes from 3DExcite Deltagen or Autodesk VRED.

Describes special considerations that apply only when you use Datasmith to bring scenes from Autodesk Navisworks into the Unreal Editor.

Describes special considerations that apply only when you use Datasmith to bring scenes from Autodesk Revit into the Unreal Editor.

Describes special considerations that apply when you use Datasmith to import scenes from McNeel Rhinoceros 3D.

Describes special considerations that apply only when you use Datasmith to bring scenes from Trimble SketchUp Pro into the Unreal Editor.

Describes how to install the Datasmith Solidworks Exporter plugin, how to get Solidworks content into Unreal Engine, and how Datasmith coverts Solidworks content.

Describes special considerations that apply when you use Datasmith to import content from CAD file formats.

Describes special considerations that apply only when you use Datasmith to bring scenes from IFC files into the Unreal Editor.

Datasmith Supported Platforms

Details what Datasmith features work on which different platforms.

Datasmith Supported Software and File Types

Details all the third-party software applications and data formats that Datasmith works with.



---

## DataValidation

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DataValidation

**Contents:**
- DataValidation
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## DaySequenceEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DaySequenceEditor

**Contents:**
- DaySequenceEditor
- Navigation
- Classes
- Interfaces



---

## DaySequence

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DaySequence

**Contents:**
- DaySequence
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

bool operator! ( ADaySequenceActor::EUpdateRootSequenceMode E )

ADaySequenceActor::EUpdateRootSequenceMode operator& ( ADaySequenceActor::EUpdateRootSequenceMode Lhs, ADaySequenceActor::EUpdateRootSequenceMode Rhs )

ADaySequenceActor::EUpdateRootSequenceMode & operator&= ( ADaySequenceActor::EUpdateRootSequenceMode& Lhs, ADaySequenceActor::EUpdateRootSequenceMode Rhs )

ADaySequenceActor::EUpdateRootSequenceMode operator^ ( ADaySequenceActor::EUpdateRootSequenceMode Lhs, ADaySequenceActor::EUpdateRootSequenceMode Rhs )

ADaySequenceActor::EUpdateRootSequenceMode & operator^= ( ADaySequenceActor::EUpdateRootSequenceMode& Lhs, ADaySequenceActor::EUpdateRootSequenceMode Rhs )

ADaySequenceActor::EUpdateRootSequenceMode operator| ( ADaySequenceActor::EUpdateRootSequenceMode Lhs, ADaySequenceActor::EUpdateRootSequenceMode Rhs )

ADaySequenceActor::EUpdateRootSequenceMode & operator|= ( ADaySequenceActor::EUpdateRootSequenceMode& Lhs, ADaySequenceActor::EUpdateRootSequenceMode Rhs )

ADaySequenceActor::EUpdateRootSequenceMode operator~ ( ADaySequenceActor::EUpdateRootSequenceMode E )

T * UE::DaySequence::GetComponentByName ( AActor* InActor, FName Name )



---

## DecoupledOutputProvider

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DecoupledOutputProvider

**Contents:**
- DecoupledOutputProvider
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## DefaultInstallBundleManager

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DefaultInstallBundleManager

**Contents:**
- DefaultInstallBundleManager
- Navigation
- Classes
- Structs
- Functions
  - Public

ENUM_RANGE_BY_COUNT ( FDefaultInstallBundleManager::EContentRequestBatch, FDefaultInstallBundleManager::EContentRequestBatch::Count )

ENUM_RANGE_BY_COUNT ( FDefaultInstallBundleManager::EContentReleaseRequestBatch, FDefaultInstallBundleManager::EContentReleaseRequestBatch::Count )

const TCHAR * LexToString ( FDefaultInstallBundleManager::EContentRequestBatch Val )

const TCHAR * LexToString ( FDefaultInstallBundleManager::EContentReleaseRequestBatch Val )



---

## DetailPoseModelEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DetailPoseModelEditor

**Contents:**
- DetailPoseModelEditor
- Navigation
- Classes
- Enums
  - Public



---

## DetailPoseModel

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DetailPoseModel

**Contents:**
- DetailPoseModel
- Navigation
- Classes
- Structs



---

## DirectLinkExtensionEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DirectLinkExtensionEditor

**Contents:**
- DirectLinkExtensionEditor
- Navigation
- Classes
- Interfaces



---

## DirectLinkExtension

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DirectLinkExtension

**Contents:**
- DirectLinkExtension
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## DirectLinkTest

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DirectLinkTest

**Contents:**
- DirectLinkTest
- Navigation
- Classes



---

## DirectoryPlaceholder

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DirectoryPlaceholder

**Contents:**
- DirectoryPlaceholder
- Navigation
- Classes



---

## DisasterRecoveryClient

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisasterRecoveryClient

**Contents:**
- DisasterRecoveryClient
- Navigation
- Interfaces



---

## DiscoveryBeaconReceiver

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DiscoveryBeaconReceiver

**Contents:**
- DiscoveryBeaconReceiver
- Navigation
- Classes



---

## DisplayClusterColorGrading

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterColorGrading

**Contents:**
- DisplayClusterColorGrading
- Navigation
- Interfaces



---

## DisplayClusterConfiguration

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterConfiguration

**Contents:**
- DisplayClusterConfiguration
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Constants
- Functions
  - Static

static const TCHAR * DisplayClusterConfiguration::GetCurrentConfigurationSchemeMarker()



---

## DisplayClusterConfigurator

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterConfigurator

**Contents:**
- DisplayClusterConfigurator
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

UDisplayClusterConfigurationClusterNode * UE::DisplayClusterConfiguratorClusterUtils::AddClusterNodeToCluster ( UDisplayClusterConfigurationClusterNode* ClusterNode, UDisplayClusterConfigurationCluster* Cluster, FString NewClusterNodeName )

UDisplayClusterConfigurationViewport * UE::DisplayClusterConfiguratorClusterUtils::AddViewportToClusterNode ( UDisplayClusterConfigurationViewport* Viewport, UDisplayClusterConfigurationClusterNode* ClusterNode, FString NewViewportName )

UDisplayClusterConfigurationHostDisplayData * UE::DisplayClusterConfiguratorClusterUtils::FindOrCreateHostDisplayData ( UDisplayClusterConfigurationCluster* Cluster, FString HostIPAddress )

FString UE::DisplayClusterConfiguratorClusterUtils::GetAddressForHost ( UDisplayClusterConfigurationHostDisplayData* HostDisplayData )

FString UE::DisplayClusterConfiguratorClusterUtils::GetClusterNodeName ( UDisplayClusterConfigurationClusterNode* ClusterNode )

UDisplayClusterConfigurationHostDisplayData * UE::DisplayClusterConfiguratorClusterUtils::GetHostDisplayDataForClusterNode ( UDisplayClusterConfigurationClusterNode* ClusterNode )

FString UE::DisplayClusterConfiguratorClusterUtils::GetUniqueNameForClusterNode ( FString InitialName, UDisplayClusterConfigurationCluster* ParentCluster, bool bAddZero )

FString UE::DisplayClusterConfiguratorClusterUtils::GetUniqueNameForHost ( FString InitialName, UDisplayClusterConfigurationCluster* ParentCluster, bool bAddZero )

FString UE::DisplayClusterConfiguratorClusterUtils::GetUniqueNameForViewport ( FString InitialName, UDisplayClusterConfigurationClusterNode* ParentClusterNode, bool bAddZero )

FString UE::DisplayClusterConfiguratorClusterUtils::GetViewportName ( UDisplayClusterConfigurationViewport* Viewport )

bool UE::DisplayClusterConfiguratorClusterUtils::IsClusterNodePrimary ( UDisplayClusterConfigurationClusterNode* ClusterNode )

bool UE::DisplayClusterConfiguratorClusterUtils::RemoveClusterNodeFromCluster ( UDisplayClusterConfigurationClusterNode* ClusterNode )

bool UE::DisplayClusterConfiguratorClusterUtils::RemoveHost ( UDisplayClusterConfigurationCluster* Cluster, FString Host )

bool UE::DisplayClusterConfiguratorClusterUtils::RemoveUnusedHostDisplayData ( UDisplayClusterConfigurationCluster* Cluster )

bool UE::DisplayClusterConfiguratorClusterUtils::RemoveViewportFromClusterNode ( UDisplayClusterConfigurationViewport* Viewport )

bool UE::DisplayClusterConfiguratorClusterUtils::RenameClusterNode ( UDisplayClusterConfigurationClusterNode* ClusterNode, FString NewClusterNodeName )

bool UE::DisplayClusterConfiguratorClusterUtils::RenameViewport ( UDisplayClusterConfigurationViewport* Viewport, FString NewViewportName )

bool UE::DisplayClusterConfiguratorClusterUtils::SetClusterNodeAsPrimary ( UDisplayClusterConfigurationClusterNode* ClusterNode )

void UE::DisplayClusterConfiguratorClusterUtils::SortClusterNodesByHost ( const TMap< FString, UDisplayClusterConfigurationClusterNode* >& InClusterNodes, TMap< FString, TMap< FString, UDisplayClusterConfigurationClusterNode* > >& OutSortedNodes )

void UE::DisplayClusterConfiguratorClusterUtils::SortClusterNodesByHost ( const TMap< FString, TObjectPtr< UDisplayClusterConfigurationClusterNode > >& InClusterNodes, TMap< FString, TMap< FString, UDisplayClusterConfigurationClusterNode* > >& OutSortedNodes )



---

## DisplayClusterDetails

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterDetails

**Contents:**
- DisplayClusterDetails
- Navigation
- Interfaces



---

## DisplayClusterEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterEditor

**Contents:**
- DisplayClusterEditor
- Navigation
- Classes
- Interfaces



---

## DisplayClusterFillDerivedDataCache

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterFillDerivedDataCac-

**Contents:**
- DisplayClusterFillDerivedDataCache
- Navigation
- Classes
- Structs
- Constants



---

## DisplayClusterLaunchEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterLaunchEditor

**Contents:**
- DisplayClusterLaunchEditor
- Navigation
- Classes
- Structs
- Enums
  - Public
- Constants



---

## DisplayClusterLightCardEditorShaders

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterLightCardEditorSha-

**Contents:**
- DisplayClusterLightCardEditorShaders
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## DisplayClusterLightCardEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterLightCardEditor

**Contents:**
- DisplayClusterLightCardEditor
- Navigation
- Interfaces



---

## DisplayClusterLightCardExtender

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterLightCardExtender

**Contents:**
- DisplayClusterLightCardExtender
- Navigation
- Classes
- Structs
- Interfaces



---

## DisplayClusterMedia

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterMedia

**Contents:**
- DisplayClusterMedia
- Navigation
- Classes



---

## DisplayClusterMessageInterception

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterMessageInterceptio-

**Contents:**
- DisplayClusterMessageInterception
- Navigation
- Classes
- Structs



---

## DisplayClusterModularFeaturesEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterModularFeaturesEdi-

**Contents:**
- DisplayClusterModularFeaturesEditor
- Navigation
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

bool operator! ( EMediaStreamPropagationType E )

EMediaStreamPropagationType operator& ( EMediaStreamPropagationType Lhs, EMediaStreamPropagationType Rhs )

EMediaStreamPropagationType & operator&= ( EMediaStreamPropagationType& Lhs, EMediaStreamPropagationType Rhs )

EMediaStreamPropagationType operator^ ( EMediaStreamPropagationType Lhs, EMediaStreamPropagationType Rhs )

EMediaStreamPropagationType & operator^= ( EMediaStreamPropagationType& Lhs, EMediaStreamPropagationType Rhs )

EMediaStreamPropagationType operator| ( EMediaStreamPropagationType Lhs, EMediaStreamPropagationType Rhs )

EMediaStreamPropagationType & operator|= ( EMediaStreamPropagationType& Lhs, EMediaStreamPropagationType Rhs )

EMediaStreamPropagationType operator~ ( EMediaStreamPropagationType E )



---

## DisplayClusterMoviePipelineEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterMoviePipelineEdito-

**Contents:**
- DisplayClusterMoviePipelineEditor
- Navigation
- Interfaces



---

## DisplayClusterMoviePipeline

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterMoviePipeline

**Contents:**
- DisplayClusterMoviePipeline
- Navigation
- Classes
- Structs



---

## DisplayClusterOperator

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterOperator

**Contents:**
- DisplayClusterOperator
- Navigation
- Classes
- Interfaces



---

## DisplayClusterProjection

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterProjection

**Contents:**
- DisplayClusterProjection
- Navigation
- Classes
- Structs
- Interfaces
- Constants
- Functions
  - Static

static EDisplayClusterWarpProfileType UE::DisplayClusterProjectionHelpers::MPCDI::ProfileTypeFromString ( const FString& InProfileTypeName )

static FString UE::DisplayClusterProjectionHelpers::MPCDI::ProfileTypeToString ( const EDisplayClusterWarpProfileType InProfileType )



---

## DisplayClusterReplication

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterReplication

**Contents:**
- DisplayClusterReplication
- Navigation
- Classes
- Structs



---

## DisplayClusterScenePreview

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterScenePreview

**Contents:**
- DisplayClusterScenePreview
- Navigation
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

bool operator! ( EDisplayClusterScenePreviewFlags E )

EDisplayClusterScenePreviewFlags operator& ( EDisplayClusterScenePreviewFlags Lhs, EDisplayClusterScenePreviewFlags Rhs )

EDisplayClusterScenePreviewFlags & operator&= ( EDisplayClusterScenePreviewFlags& Lhs, EDisplayClusterScenePreviewFlags Rhs )

EDisplayClusterScenePreviewFlags operator^ ( EDisplayClusterScenePreviewFlags Lhs, EDisplayClusterScenePreviewFlags Rhs )

EDisplayClusterScenePreviewFlags & operator^= ( EDisplayClusterScenePreviewFlags& Lhs, EDisplayClusterScenePreviewFlags Rhs )

EDisplayClusterScenePreviewFlags operator| ( EDisplayClusterScenePreviewFlags Lhs, EDisplayClusterScenePreviewFlags Rhs )

EDisplayClusterScenePreviewFlags & operator|= ( EDisplayClusterScenePreviewFlags& Lhs, EDisplayClusterScenePreviewFlags Rhs )

EDisplayClusterScenePreviewFlags operator~ ( EDisplayClusterScenePreviewFlags E )



---

## DisplayClusterShaders

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterShaders

**Contents:**
- DisplayClusterShaders
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

bool operator! ( EDisplayClusterShaderTextureUtilsFlags E )

EDisplayClusterShaderTextureUtilsFlags operator& ( EDisplayClusterShaderTextureUtilsFlags Lhs, EDisplayClusterShaderTextureUtilsFlags Rhs )

EDisplayClusterShaderTextureUtilsFlags & operator&= ( EDisplayClusterShaderTextureUtilsFlags& Lhs, EDisplayClusterShaderTextureUtilsFlags Rhs )

EDisplayClusterShaderTextureUtilsFlags operator^ ( EDisplayClusterShaderTextureUtilsFlags Lhs, EDisplayClusterShaderTextureUtilsFlags Rhs )

EDisplayClusterShaderTextureUtilsFlags & operator^= ( EDisplayClusterShaderTextureUtilsFlags& Lhs, EDisplayClusterShaderTextureUtilsFlags Rhs )

EDisplayClusterShaderTextureUtilsFlags operator| ( EDisplayClusterShaderTextureUtilsFlags Lhs, EDisplayClusterShaderTextureUtilsFlags Rhs )

EDisplayClusterShaderTextureUtilsFlags & operator|= ( EDisplayClusterShaderTextureUtilsFlags& Lhs, EDisplayClusterShaderTextureUtilsFlags Rhs )

EDisplayClusterShaderTextureUtilsFlags operator~ ( EDisplayClusterShaderTextureUtilsFlags E )



---

## DisplayClusterWarp

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayClusterWarp

**Contents:**
- DisplayClusterWarp
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Constants
- Functions
  - Public

bool operator! ( EDisplayClusterWarpMPCDIAttributesFlags E )

EDisplayClusterWarpMPCDIAttributesFlags operator& ( EDisplayClusterWarpMPCDIAttributesFlags Lhs, EDisplayClusterWarpMPCDIAttributesFlags Rhs )

EDisplayClusterWarpMPCDIAttributesFlags & operator&= ( EDisplayClusterWarpMPCDIAttributesFlags& Lhs, EDisplayClusterWarpMPCDIAttributesFlags Rhs )

EDisplayClusterWarpMPCDIAttributesFlags operator^ ( EDisplayClusterWarpMPCDIAttributesFlags Lhs, EDisplayClusterWarpMPCDIAttributesFlags Rhs )

EDisplayClusterWarpMPCDIAttributesFlags & operator^= ( EDisplayClusterWarpMPCDIAttributesFlags& Lhs, EDisplayClusterWarpMPCDIAttributesFlags Rhs )

EDisplayClusterWarpMPCDIAttributesFlags operator| ( EDisplayClusterWarpMPCDIAttributesFlags Lhs, EDisplayClusterWarpMPCDIAttributesFlags Rhs )

EDisplayClusterWarpMPCDIAttributesFlags & operator|= ( EDisplayClusterWarpMPCDIAttributesFlags& Lhs, EDisplayClusterWarpMPCDIAttributesFlags Rhs )

EDisplayClusterWarpMPCDIAttributesFlags operator~ ( EDisplayClusterWarpMPCDIAttributesFlags E )



---

## DisplayCluster

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DisplayCluster

**Contents:**
- DisplayCluster
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

bool DisplayClusterHelpers::map::ExtractArrayFromString ( const TMap< FString, FString >& InMap, const FString& InKey, TArray< TVal >& OutArray, const FString& InSeparator, bool bCullEmpty, ESearchCase::Type SearchCase )

bool DisplayClusterHelpers::map::ExtractMapFromString ( const TMap< FString, FString >& InMap, const FString& InKey, TMap< TKey, TVal >& OutMap, const FString& InPairSeparator, const FString& InKeyValSeparator, ESearchCase::Type SearchCase )

bool DisplayClusterHelpers::map::ExtractValue ( const TMap< FString, TVal >& InMap, const FString& InKey, TVal& OutValue, ESearchCase::Type SearchCase )

TVal DisplayClusterHelpers::map::ExtractValue ( const TMap< FString, TVal >& InMap, const FString& InKey, const TVal& DefaultValue, ESearchCase::Type SearchCase )

bool DisplayClusterHelpers::map::ExtractValueFromString ( const TMap< FString, FString >& InMap, const FString& InKey, TReturn& OutValue, ESearchCase::Type SearchCase )

TReturn DisplayClusterHelpers::map::ExtractValueFromString ( const TMap< FString, FString >& InMap, const FString& InKey, const TReturn& DefaultValue, ESearchCase::Type SearchCase )

FString DisplayClusterHelpers::str::MapToStr ( const TMap< TKey, TVal >& InData, const FString& InPairSeparator, const FString& InKeyValSeparator, bool bAddQuoutes )

void DisplayClusterHelpers::str::StrToMap ( const FString& InData, TMap< TKey, TVal >& OutData, const FString& InPairSeparator, const FString& InKeyValSeparator )

bool operator! ( EDisplayClusterLabelFlags E )

bool operator! ( EDisplayClusterProjectionPolicyFlags E )

bool operator! ( EDisplayClusterRootActorType E )

bool operator! ( EDisplayClusterViewportMediaState E )

bool operator! ( EDisplayClusterViewportCameraPostProcessFlags E )

bool operator! ( EDisplayClusterViewportRenderingFlags E )

bool operator! ( EDisplayClusterViewportICVFXFlags E )

bool operator! ( EDisplayClusterViewportRuntimeICVFXFlags E )

bool operator! ( EDisplayClusterViewportTileFlags E )

bool operator! ( EDisplayClusterViewportPreviewFlags E )

EDisplayClusterLabelFlags operator& ( EDisplayClusterLabelFlags Lhs, EDisplayClusterLabelFlags Rhs )

EDisplayClusterProjectionPolicyFlags operator& ( EDisplayClusterProjectionPolicyFlags Lhs, EDisplayClusterProjectionPolicyFlags Rhs )

EDisplayClusterRootActorType operator& ( EDisplayClusterRootActorType Lhs, EDisplayClusterRootActorType Rhs )

EDisplayClusterViewportMediaState operator& ( EDisplayClusterViewportMediaState Lhs, EDisplayClusterViewportMediaState Rhs )

EDisplayClusterViewportCameraPostProcessFlags operator& ( EDisplayClusterViewportCameraPostProcessFlags Lhs, EDisplayClusterViewportCameraPostProcessFlags Rhs )

EDisplayClusterViewportRenderingFlags operator& ( EDisplayClusterViewportRenderingFlags Lhs, EDisplayClusterViewportRenderingFlags Rhs )

EDisplayClusterViewportICVFXFlags operator& ( EDisplayClusterViewportICVFXFlags Lhs, EDisplayClusterViewportICVFXFlags Rhs )

EDisplayClusterViewportRuntimeICVFXFlags operator& ( EDisplayClusterViewportRuntimeICVFXFlags Lhs, EDisplayClusterViewportRuntimeICVFXFlags Rhs )

EDisplayClusterViewportTileFlags operator& ( EDisplayClusterViewportTileFlags Lhs, EDisplayClusterViewportTileFlags Rhs )

EDisplayClusterViewportPreviewFlags operator& ( EDisplayClusterViewportPreviewFlags Lhs, EDisplayClusterViewportPreviewFlags Rhs )

EDisplayClusterLabelFlags & operator&= ( EDisplayClusterLabelFlags& Lhs, EDisplayClusterLabelFlags Rhs )

EDisplayClusterProjectionPolicyFlags & operator&= ( EDisplayClusterProjectionPolicyFlags& Lhs, EDisplayClusterProjectionPolicyFlags Rhs )

EDisplayClusterRootActorType & operator&= ( EDisplayClusterRootActorType& Lhs, EDisplayClusterRootActorType Rhs )

EDisplayClusterViewportMediaState & operator&= ( EDisplayClusterViewportMediaState& Lhs, EDisplayClusterViewportMediaState Rhs )

EDisplayClusterViewportCameraPostProcessFlags & operator&= ( EDisplayClusterViewportCameraPostProcessFlags& Lhs, EDisplayClusterViewportCameraPostProcessFlags Rhs )

EDisplayClusterViewportRenderingFlags & operator&= ( EDisplayClusterViewportRenderingFlags& Lhs, EDisplayClusterViewportRenderingFlags Rhs )

EDisplayClusterViewportICVFXFlags & operator&= ( EDisplayClusterViewportICVFXFlags& Lhs, EDisplayClusterViewportICVFXFlags Rhs )

EDisplayClusterViewportRuntimeICVFXFlags & operator&= ( EDisplayClusterViewportRuntimeICVFXFlags& Lhs, EDisplayClusterViewportRuntimeICVFXFlags Rhs )

EDisplayClusterViewportTileFlags & operator&= ( EDisplayClusterViewportTileFlags& Lhs, EDisplayClusterViewportTileFlags Rhs )

EDisplayClusterViewportPreviewFlags & operator&= ( EDisplayClusterViewportPreviewFlags& Lhs, EDisplayClusterViewportPreviewFlags Rhs )

EDisplayClusterLabelFlags operator^ ( EDisplayClusterLabelFlags Lhs, EDisplayClusterLabelFlags Rhs )

EDisplayClusterProjectionPolicyFlags operator^ ( EDisplayClusterProjectionPolicyFlags Lhs, EDisplayClusterProjectionPolicyFlags Rhs )

EDisplayClusterRootActorType operator^ ( EDisplayClusterRootActorType Lhs, EDisplayClusterRootActorType Rhs )

EDisplayClusterViewportMediaState operator^ ( EDisplayClusterViewportMediaState Lhs, EDisplayClusterViewportMediaState Rhs )

EDisplayClusterViewportCameraPostProcessFlags operator^ ( EDisplayClusterViewportCameraPostProcessFlags Lhs, EDisplayClusterViewportCameraPostProcessFlags Rhs )

EDisplayClusterViewportRenderingFlags operator^ ( EDisplayClusterViewportRenderingFlags Lhs, EDisplayClusterViewportRenderingFlags Rhs )

EDisplayClusterViewportICVFXFlags operator^ ( EDisplayClusterViewportICVFXFlags Lhs, EDisplayClusterViewportICVFXFlags Rhs )

EDisplayClusterViewportRuntimeICVFXFlags operator^ ( EDisplayClusterViewportRuntimeICVFXFlags Lhs, EDisplayClusterViewportRuntimeICVFXFlags Rhs )

EDisplayClusterViewportTileFlags operator^ ( EDisplayClusterViewportTileFlags Lhs, EDisplayClusterViewportTileFlags Rhs )

EDisplayClusterViewportPreviewFlags operator^ ( EDisplayClusterViewportPreviewFlags Lhs, EDisplayClusterViewportPreviewFlags Rhs )

EDisplayClusterLabelFlags & operator^= ( EDisplayClusterLabelFlags& Lhs, EDisplayClusterLabelFlags Rhs )

EDisplayClusterProjectionPolicyFlags & operator^= ( EDisplayClusterProjectionPolicyFlags& Lhs, EDisplayClusterProjectionPolicyFlags Rhs )

EDisplayClusterRootActorType & operator^= ( EDisplayClusterRootActorType& Lhs, EDisplayClusterRootActorType Rhs )

EDisplayClusterViewportMediaState & operator^= ( EDisplayClusterViewportMediaState& Lhs, EDisplayClusterViewportMediaState Rhs )

EDisplayClusterViewportCameraPostProcessFlags & operator^= ( EDisplayClusterViewportCameraPostProcessFlags& Lhs, EDisplayClusterViewportCameraPostProcessFlags Rhs )

EDisplayClusterViewportRenderingFlags & operator^= ( EDisplayClusterViewportRenderingFlags& Lhs, EDisplayClusterViewportRenderingFlags Rhs )

EDisplayClusterViewportICVFXFlags & operator^= ( EDisplayClusterViewportICVFXFlags& Lhs, EDisplayClusterViewportICVFXFlags Rhs )

EDisplayClusterViewportRuntimeICVFXFlags & operator^= ( EDisplayClusterViewportRuntimeICVFXFlags& Lhs, EDisplayClusterViewportRuntimeICVFXFlags Rhs )

EDisplayClusterViewportTileFlags & operator^= ( EDisplayClusterViewportTileFlags& Lhs, EDisplayClusterViewportTileFlags Rhs )

EDisplayClusterViewportPreviewFlags & operator^= ( EDisplayClusterViewportPreviewFlags& Lhs, EDisplayClusterViewportPreviewFlags Rhs )

EDisplayClusterLabelFlags operator| ( EDisplayClusterLabelFlags Lhs, EDisplayClusterLabelFlags Rhs )

EDisplayClusterProjectionPolicyFlags operator| ( EDisplayClusterProjectionPolicyFlags Lhs, EDisplayClusterProjectionPolicyFlags Rhs )

EDisplayClusterRootActorType operator| ( EDisplayClusterRootActorType Lhs, EDisplayClusterRootActorType Rhs )

EDisplayClusterViewportMediaState operator| ( EDisplayClusterViewportMediaState Lhs, EDisplayClusterViewportMediaState Rhs )

EDisplayClusterViewportCameraPostProcessFlags operator| ( EDisplayClusterViewportCameraPostProcessFlags Lhs, EDisplayClusterViewportCameraPostProcessFlags Rhs )

EDisplayClusterViewportRenderingFlags operator| ( EDisplayClusterViewportRenderingFlags Lhs, EDisplayClusterViewportRenderingFlags Rhs )

EDisplayClusterViewportICVFXFlags operator| ( EDisplayClusterViewportICVFXFlags Lhs, EDisplayClusterViewportICVFXFlags Rhs )

EDisplayClusterViewportRuntimeICVFXFlags operator| ( EDisplayClusterViewportRuntimeICVFXFlags Lhs, EDisplayClusterViewportRuntimeICVFXFlags Rhs )

EDisplayClusterViewportTileFlags operator| ( EDisplayClusterViewportTileFlags Lhs, EDisplayClusterViewportTileFlags Rhs )

EDisplayClusterViewportPreviewFlags operator| ( EDisplayClusterViewportPreviewFlags Lhs, EDisplayClusterViewportPreviewFlags Rhs )

EDisplayClusterLabelFlags & operator|= ( EDisplayClusterLabelFlags& Lhs, EDisplayClusterLabelFlags Rhs )

EDisplayClusterProjectionPolicyFlags & operator|= ( EDisplayClusterProjectionPolicyFlags& Lhs, EDisplayClusterProjectionPolicyFlags Rhs )

EDisplayClusterRootActorType & operator|= ( EDisplayClusterRootActorType& Lhs, EDisplayClusterRootActorType Rhs )

EDisplayClusterViewportMediaState & operator|= ( EDisplayClusterViewportMediaState& Lhs, EDisplayClusterViewportMediaState Rhs )

EDisplayClusterViewportCameraPostProcessFlags & operator|= ( EDisplayClusterViewportCameraPostProcessFlags& Lhs, EDisplayClusterViewportCameraPostProcessFlags Rhs )

EDisplayClusterViewportRenderingFlags & operator|= ( EDisplayClusterViewportRenderingFlags& Lhs, EDisplayClusterViewportRenderingFlags Rhs )

EDisplayClusterViewportICVFXFlags & operator|= ( EDisplayClusterViewportICVFXFlags& Lhs, EDisplayClusterViewportICVFXFlags Rhs )

EDisplayClusterViewportRuntimeICVFXFlags & operator|= ( EDisplayClusterViewportRuntimeICVFXFlags& Lhs, EDisplayClusterViewportRuntimeICVFXFlags Rhs )

EDisplayClusterViewportTileFlags & operator|= ( EDisplayClusterViewportTileFlags& Lhs, EDisplayClusterViewportTileFlags Rhs )

EDisplayClusterViewportPreviewFlags & operator|= ( EDisplayClusterViewportPreviewFlags& Lhs, EDisplayClusterViewportPreviewFlags Rhs )

EDisplayClusterLabelFlags operator~ ( EDisplayClusterLabelFlags E )

EDisplayClusterProjectionPolicyFlags operator~ ( EDisplayClusterProjectionPolicyFlags E )

EDisplayClusterRootActorType operator~ ( EDisplayClusterRootActorType E )

EDisplayClusterViewportMediaState operator~ ( EDisplayClusterViewportMediaState E )

EDisplayClusterViewportCameraPostProcessFlags operator~ ( EDisplayClusterViewportCameraPostProcessFlags E )

EDisplayClusterViewportRenderingFlags operator~ ( EDisplayClusterViewportRenderingFlags E )

EDisplayClusterViewportICVFXFlags operator~ ( EDisplayClusterViewportICVFXFlags E )

EDisplayClusterViewportRuntimeICVFXFlags operator~ ( EDisplayClusterViewportRuntimeICVFXFlags E )

EDisplayClusterViewportTileFlags operator~ ( EDisplayClusterViewportTileFlags E )

EDisplayClusterViewportPreviewFlags operator~ ( EDisplayClusterViewportPreviewFlags E )

const TComp & UE::DisplayClusterViewportHelpers::GetMatchingComponentFromRootActor ( const IDisplayClusterViewportConfiguration& InConfiguration, const EDisplayClusterRootActorType InRootActorType, const TComp& InComponent )

TComp * UE::DisplayClusterViewportHelpers::GetOwnerRootActorComponentByName ( USceneComponent* ComponentOfRootActor, const FString& InComponentName )

TComp * UE::DisplayClusterViewportHelpers::GetRootActorComponentByName ( const IDisplayClusterViewportConfiguration& InConfiguration, const EDisplayClusterRootActorType InRootActorType, const FString& InComponentName )

static FString DisplayClusterHelpers::filesystem::GetFullPathForConfig ( const FString& RelativeConfig )

static FString DisplayClusterHelpers::filesystem::GetFullPathForConfigResource ( const FString& ResourcePath )

static FString DisplayClusterHelpers::filesystem::GetFullPathForThirdPartyDLL ( const FString& InRelativePathForThirdPartyDll )

static TArray< FString > DisplayClusterHelpers::filesystem::GetOrderedConfigResourceDirs()

static FString DisplayClusterHelpers::filesystem::GetRelativePathForConfigResource ( const FString& ResourceFullPath )

static void DisplayClusterHelpers::game::FindAllActors ( UWorld* World, TArray< T* >& Out )

static FString DisplayClusterHelpers::str::ArrayToStr ( const TArray< TVal >& InData, const FString& InSeparator, bool bAddQuotes )

static FString DisplayClusterHelpers::str::BoolToStr ( bool bVal, bool bAsWord )

static bool DisplayClusterHelpers::str::ExtractArray ( const FString& InLine, const FString& InParamName, const FString& InSeparator, TArray< TVal >& OutValue )

static bool DisplayClusterHelpers::str::ExtractMap ( const FString& InLine, const FString& InParamName, TMap< TKey, TVal >& OutData, const FString& InPairSeparator, const FString& InKeyValSeparator )

static bool DisplayClusterHelpers::str::ExtractValue ( const FString& InLine, const FString& InParamName, T& OutValue, bool bInTrimQuotes )

static FString DisplayClusterHelpers::str::SetToStr ( const TSet< TVal >& InData, const FString& InSeparator, bool bAddQuotes )

static void DisplayClusterHelpers::str::StrToArray ( const FString& InData, const FString& InSeparator, TArray< TVal >& OutData, bool bCullEmpty )

static void DisplayClusterHelpers::str::StrToSet ( const FString& InData, const FString& InSeparator, TSet< TVal >& OutData, bool bCullEmpty )

static void DisplayClusterHelpers::str::TrimStringValue ( FString& InLine, bool bTrimQuotes )

static FString DisplayClusterHelpers::str::TrimStringValue ( const FString& InLine, bool bTrimQuotes )



---

## DMXBlueprintGraph

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DMXBlueprintGraph

**Contents:**
- DMXBlueprintGraph
- Navigation
- Classes



---

## DMXControlConsoleEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DMXControlConsoleEditor

**Contents:**
- DMXControlConsoleEditor
- Navigation
- Interfaces



---

## DMXControlConsole

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DMXControlConsole

**Contents:**
- DMXControlConsole
- Navigation
- Classes



---

## DMXEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DMXEditor

**Contents:**
- DMXEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

class UE_DEPRECATED (



---

## DMXFixtureActorInterface

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DMXFixtureActorInterface

**Contents:**
- DMXFixtureActorInterface
- Navigation
- Classes
- Interfaces



---

## DMXFixtures

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DMXFixtures

**Contents:**
- DMXFixtures
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## DMXGDTF

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DMXGDTF

**Contents:**
- DMXGDTF
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## DMXPixelMappingBlueprintGraph

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DMXPixelMappingBlueprintGraph

**Contents:**
- DMXPixelMappingBlueprintGraph
- Navigation
- Classes



---

## DMXPixelMappingCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DMXPixelMappingCore

**Contents:**
- DMXPixelMappingCore
- Navigation
- Structs
- Enums
  - Public



---

## DMXPixelMappingEditorWidgets

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DMXPixelMappingEditorWidgets

**Contents:**
- DMXPixelMappingEditorWidgets
- Navigation
- Classes
- Structs



---

## DMXPixelMappingRenderer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DMXPixelMappingRenderer

**Contents:**
- DMXPixelMappingRenderer
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## DMXPixelMappingRuntime

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DMXPixelMappingRuntime

**Contents:**
- DMXPixelMappingRuntime
- Navigation
- Classes
- Structs
- Enums
  - Public
- Variables
  - Public



---

## DMXProtocolArtNet

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DMXProtocolArtNet

**Contents:**
- DMXProtocolArtNet
- Navigation
- Classes



---

## DMXProtocolBlueprintGraph

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DMXProtocolBlueprintGraph

**Contents:**
- DMXProtocolBlueprintGraph
- Navigation
- Classes



---

## DMXProtocolEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DMXProtocolEditor

**Contents:**
- DMXProtocolEditor
- Navigation
- Classes
- Enums
  - Public



---

## DMXProtocolsACN

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DMXProtocolsACN

**Contents:**
- DMXProtocolsACN
- Navigation
- Classes



---

## DMXProtocol

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DMXProtocol

**Contents:**
- DMXProtocol
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

uint32 GetTypeHash ( const FDMXAttribute& Attribute )

uint32 GetTypeHash ( const FDMXAttributeName& DMXNameListItem )

bool operator!= ( const FDMXAttributeName& V1, const FDMXAttributeName& V2 )

bool operator== ( const FDMXAttributeName& V1, const FDMXAttributeName& V2 )



---

## DMXRuntime

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DMXRuntime

**Contents:**
- DMXRuntime
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Constants
- Variables
  - Public

FDMXColorCIE UE::DMX::DMXImport::Private::ParseColorCIE ( const FString& InColor )

FMatrix UE::DMX::DMXImport::Private::ParseMatrix ( FString&& InMatrixStr )

static EnumType UE::DMX::DMXImport::Private::GetEnumValueFromString ( const FString& String )



---

## DMXZip

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DMXZip

**Contents:**
- DMXZip
- Navigation
- Classes



---

## DNACalibLibTest

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DNACalibLibTest

**Contents:**
- DNACalibLibTest
- Navigation
- Classes



---

## DNACalibLib

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DNACalibLib

**Contents:**
- DNACalibLib
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Functions
  - Public

ConditionalCommand< TCommand, TCondition > dnac::makeConditional ( TCommand* command, TCondition condition )



---

## DNACalibModule

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DNACalibModule

**Contents:**
- DNACalibModule
- Navigation
- Classes
- Interfaces
- Enums
  - Public



---

## DrawDebugLibrary

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DrawDebugLibrary

**Contents:**
- DrawDebugLibrary
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## DTLSHandlerComponent

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DTLSHandlerComponent

**Contents:**
- DTLSHandlerComponent
- Navigation
- Classes



---

## DummyMeshReconstructor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DummyMeshReconstructor

**Contents:**
- DummyMeshReconstructor
- Navigation
- Classes



---

## DumpGPUServices

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DumpGPUServices

**Contents:**
- DumpGPUServices
- Navigation
- Interfaces



---

## DynamicMaterialEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DynamicMaterialEditor

**Contents:**
- DynamicMaterialEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

bool operator! ( EDMMaterialLayerStage E )

bool operator! ( EAvaColorChannel E )

EDMMaterialLayerStage operator& ( EDMMaterialLayerStage Lhs, EDMMaterialLayerStage Rhs )

EAvaColorChannel operator& ( EAvaColorChannel Lhs, EAvaColorChannel Rhs )

EDMMaterialLayerStage & operator&= ( EDMMaterialLayerStage& Lhs, EDMMaterialLayerStage Rhs )

EAvaColorChannel & operator&= ( EAvaColorChannel& Lhs, EAvaColorChannel Rhs )

EDMMaterialLayerStage operator^ ( EDMMaterialLayerStage Lhs, EDMMaterialLayerStage Rhs )

EAvaColorChannel operator^ ( EAvaColorChannel Lhs, EAvaColorChannel Rhs )

EDMMaterialLayerStage & operator^= ( EDMMaterialLayerStage& Lhs, EDMMaterialLayerStage Rhs )

EAvaColorChannel & operator^= ( EAvaColorChannel& Lhs, EAvaColorChannel Rhs )

EDMMaterialLayerStage operator| ( EDMMaterialLayerStage Lhs, EDMMaterialLayerStage Rhs )

EAvaColorChannel operator| ( EAvaColorChannel Lhs, EAvaColorChannel Rhs )

EDMMaterialLayerStage & operator|= ( EDMMaterialLayerStage& Lhs, EDMMaterialLayerStage Rhs )

EAvaColorChannel & operator|= ( EAvaColorChannel& Lhs, EAvaColorChannel Rhs )

EDMMaterialLayerStage operator~ ( EDMMaterialLayerStage E )

EAvaColorChannel operator~ ( EAvaColorChannel E )



---

## DynamicMaterialMediaStreamBridge

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DynamicMaterialMediaStreamBridge

**Contents:**
- DynamicMaterialMediaStreamBridge
- Navigation
- Classes



---

## DynamicMaterialShaders

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DynamicMaterialShaders

**Contents:**
- DynamicMaterialShaders
- Navigation
- Classes
- Typedefs



---

## DynamicMaterialTextureSetEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DynamicMaterialTextureSetEditor

**Contents:**
- DynamicMaterialTextureSetEditor
- Navigation
- Classes
- Typedefs



---

## DynamicMaterialTextureSet

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DynamicMaterialTextureSet

**Contents:**
- DynamicMaterialTextureSet
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

bool operator! ( EDMTextureChannelMask E )

EDMTextureChannelMask operator& ( EDMTextureChannelMask Lhs, EDMTextureChannelMask Rhs )

EDMTextureChannelMask & operator&= ( EDMTextureChannelMask& Lhs, EDMTextureChannelMask Rhs )

EDMTextureChannelMask operator^ ( EDMTextureChannelMask Lhs, EDMTextureChannelMask Rhs )

EDMTextureChannelMask & operator^= ( EDMTextureChannelMask& Lhs, EDMTextureChannelMask Rhs )

EDMTextureChannelMask operator| ( EDMTextureChannelMask Lhs, EDMTextureChannelMask Rhs )

EDMTextureChannelMask & operator|= ( EDMTextureChannelMask& Lhs, EDMTextureChannelMask Rhs )

EDMTextureChannelMask operator~ ( EDMTextureChannelMask E )



---

## DynamicMaterial

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DynamicMaterial

**Contents:**
- DynamicMaterial
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

bool operator! ( EDMUpdateType E )

EDMUpdateType operator& ( EDMUpdateType Lhs, EDMUpdateType Rhs )

EDMUpdateType & operator&= ( EDMUpdateType& Lhs, EDMUpdateType Rhs )

EDMUpdateType operator^ ( EDMUpdateType Lhs, EDMUpdateType Rhs )

EDMUpdateType & operator^= ( EDMUpdateType& Lhs, EDMUpdateType Rhs )

EDMUpdateType operator| ( EDMUpdateType Lhs, EDMUpdateType Rhs )

EDMUpdateType & operator|= ( EDMUpdateType& Lhs, EDMUpdateType Rhs )

EDMUpdateType operator~ ( EDMUpdateType E )

void UE::DynamicMaterial::ForEachMaterialPropertyType ( TFunctionRef< EDMIterationResult(EDMMaterialPropertyType InType)> InCallable, EDMMaterialPropertyType InStart, EDMMaterialPropertyType InEnd )



---

## DynamicMesh

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DynamicMesh

**Contents:**
- DynamicMesh
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

bool bIsSymmetricLaplacian ( const ELaplacianWeightScheme Scheme )

void FaceGroupUtil::CountAllGroups ( const FDynamicMesh3& Mesh, TArray< int32 >& GroupCountsOut )

void FaceGroupUtil::FindAllGroups ( const FDynamicMesh3& Mesh, TSet< int32 >& GroupsOut )

bool FaceGroupUtil::FindTrianglesByGroup ( FDynamicMesh3& Mesh, int32 FindGroupID, TArray< int32 >& TrianglesOut )

void FaceGroupUtil::FindTriangleSetsByGroup ( const FDynamicMesh3& Mesh, TArray< TArray< int32 > >& GroupTrisOut, int32 IgnoreGID )

bool FaceGroupUtil::HasMultipleGroups ( const FDynamicMesh3& Mesh )

void FaceGroupUtil::SeparateMeshByGroups ( FDynamicMesh3& Mesh, TArray< FDynamicMesh3 >& SplitMeshes )

void FaceGroupUtil::SeparateMeshByGroups ( FDynamicMesh3& Mesh, TArray< FDynamicMesh3 >& SplitMeshes, TArray< int32 >& GroupIDs )

void FaceGroupUtil::SetGroupID ( FDynamicMesh3& Mesh, int32 to )

void FaceGroupUtil::SetGroupID ( FDynamicMesh3& Mesh, const TArrayView< const int32 >& triangles, int32 to )

void FaceGroupUtil::SetGroupToGroup ( FDynamicMesh3& Mesh, int32 from, int32 to )

FString LaplacianSchemeName ( const ELaplacianWeightScheme Scheme )

bool UE::Geometry::AreSelectionsIdentical ( const FGeometrySelection& SelectionA, const FGeometrySelection& SelectionB )

bool UE::Geometry::CombineSelectionInPlace ( FGeometrySelection& SelectionA, const FGeometrySelection& SelectionB, EGeometrySelectionCombineModes CombineMode )

void UE::Geometry::ComputeArbitraryTrianglePatchUVs ( FDynamicMesh3& Mesh, FDynamicMeshUVOverlay& UVOverlay, const TArray< int32 >& TriangleSet )

double UE::Geometry::ComputeAverageUVScaleRatioAlongVertexPath ( const FDynamicMesh3& Mesh, const FDynamicMeshUVOverlay& UVOverlay, const TArray< int32 >& VertexPath, double* PathLengthOut, double* UVPathLengthOut )

FFrame3d UE::Geometry::ComputeFaceSelectionFrame ( const FDynamicMesh3& Mesh, const TArray< int32 >& Triangles, bool bIsDefinitelySingleComponent )

int32 UE::Geometry::ComputeGroupIDBound ( const FDynamicMesh3& Mesh, const FDynamicMeshPolygroupAttribute* Layer )

void UE::Geometry::ComputeInsetLineSegmentsFromEdges ( const FDynamicMesh3& Mesh, const TArray< int32 >& EdgeList, double InsetDistance, TArray< FLine3d >& InsetLinesOut )

bool UE::Geometry::ComputeMaterialIDRange ( const FDynamicMesh3& Mesh, FInterval1i& MaterialIDRange )

bool UE::Geometry::ComputeMaterialIDsForVertexPath ( const FDynamicMesh3& Mesh, const TArray< int32 >& VertexPath, bool bIsLoop, TArray< int32 >& EdgeMaterialIDsOut, int32 FallbackMaterialID )

void UE::Geometry::ComputeNewGroupIDsAlongEdgeLoop ( FDynamicMesh3& Mesh, const TArray< int32 >& LoopEdgeIDs, TArray< int32 >& NewLoopEdgeGroupIDsOut, TArray< int32 >& NewGroupIDsOut, TFunctionRef< bool(int32 Eid1, int32 Eid2)> EdgesShouldHaveSameGroupFunc )

void UE::Geometry::ComputeNormalsForQuadPatch ( FDynamicMesh3& Mesh, const FQuadGridPatch& QuadPatch )

bool UE::Geometry::ComputeUVIslandForQuadPatch ( FDynamicMesh3& Mesh, const FQuadGridPatch& QuadPatch, double UVScaleFactor, int UVOverlayIndex )

bool UE::Geometry::ConvertPolygroupSelectionToIncidentOverlaySelection ( const UE::Geometry::FDynamicMesh3& Mesh, const FGroupTopology& GroupTopology, const FGeometrySelection& MeshSelection, TSet< int >& TrianglesOut, TSet< int >& VerticesOut, FGeometrySelection* TriangleVertexSelectionIncidentToEdgeOrVertexSelection )

bool UE::Geometry::ConvertPolygroupSelectionToOverlaySelection ( const UE::Geometry::FDynamicMesh3& Mesh, const FPolygroupSet& GroupSet, const FGeometrySelection& MeshSelection, TSet< int >& TrianglesOut, TSet< int >& VerticesOut )

bool UE::Geometry::ConvertPolygroupSelectionToTopologySelection ( const FGeometrySelection& MeshSelection, const UE::Geometry::FDynamicMesh3& Mesh, const FGroupTopology* GroupTopology, FGroupTopologySelection& TopologySelectionOut )

bool UE::Geometry::ConvertSelection ( const UE::Geometry::FDynamicMesh3& Mesh, const FGroupTopology* GroupTopology, const FGeometrySelection& FromSelectionIn, FGeometrySelection& ToSelectionOut )

bool UE::Geometry::ConvertSelection ( const UE::Geometry::FDynamicMesh3& Mesh, const FGroupTopology* GroupTopology, const FGeometrySelection& FromSelectionIn, FGeometrySelection& ToSelectionOut, const EEnumerateSelectionConversionParams ConversionParams )

bool UE::Geometry::ConvertTriangleSelectionToOverlaySelection ( const UE::Geometry::FDynamicMesh3& Mesh, const FGeometrySelection& MeshSelection, TSet< int >& TrianglesOut, TSet< int >& VerticesOut, FGeometrySelection* TriangleVertexSelectionIncidentToEdgeSelection )

bool UE::Geometry::EnumeratePolygroupSelectionEdges ( const FGeometrySelection& MeshSelection, const UE::Geometry::FDynamicMesh3& Mesh, const UE::Geometry::FPolygroupSet& GroupSet, TFunctionRef< void(int32)> EdgeFunc )

bool UE::Geometry::EnumeratePolygroupSelectionEdges ( const FGeometrySelection& MeshSelection, const UE::Geometry::FDynamicMesh3& Mesh, const UE::Geometry::FGroupTopology& GroupTopology, TFunctionRef< void(int32)> EdgeFunc )

bool UE::Geometry::EnumeratePolygroupSelectionElements ( const FGeometrySelection& MeshSelection, const UE::Geometry::FDynamicMesh3& Mesh, const FGroupTopology* GroupTopology, TFunctionRef< void(int32, const FVector3d&)> VertexFunc, TFunctionRef< void(int32, const FSegment3d&)> EdgeFunc, TFunctionRef< void(int32, const FTriangle3d&)> TriangleFunc, const FTransform* ApplyTransform, const bool bMapFacesToEdgeLoops )

bool UE::Geometry::EnumeratePolygroupSelectionElements ( const FGeometrySelection& MeshSelection, const UE::Geometry::FDynamicMesh3& Mesh, const FGroupTopology* GroupTopology, TFunctionRef< void(int32, const FVector3d&)> VertexFunc, TFunctionRef< void(int32, const FSegment3d&)> EdgeFunc, TFunctionRef< void(int32, const FTriangle3d&)> TriangleFunc, const FTransform* ApplyTransform, const EEnumerateSelectionMapping Flags )

bool UE::Geometry::EnumeratePolygroupSelectionTriangles ( const FGeometrySelection& MeshSelection, const UE::Geometry::FDynamicMesh3& Mesh, const UE::Geometry::FPolygroupSet& GroupSet, TFunctionRef< void(int32)> TriangleFunc )

bool UE::Geometry::EnumeratePolygroupSelectionVertices ( const FGeometrySelection& GroupSelection, const UE::Geometry::FDynamicMesh3& Mesh, const FGroupTopology* GroupTopology, const FTransform& ApplyTransform, TFunctionRef< void(uint64, const FVector3d&)> VertexFunc )

bool UE::Geometry::EnumerateSelectionEdges ( const FGeometrySelection& MeshSelection, const UE::Geometry::FDynamicMesh3& Mesh, TFunctionRef< void(int32)> EdgeFunc, const UE::Geometry::FPolygroupSet* UseGroupSet )

bool UE::Geometry::EnumerateSelectionTriangles ( const FGeometrySelection& MeshSelection, const UE::Geometry::FDynamicMesh3& Mesh, TFunctionRef< void(int32)> TriangleFunc, const UE::Geometry::FPolygroupSet* UseGroupSet )

bool UE::Geometry::EnumerateTriangleSelectionEdges ( const FGeometrySelection& MeshSelection, const UE::Geometry::FDynamicMesh3& Mesh, TFunctionRef< void(int32)> EdgeFunc )

bool UE::Geometry::EnumerateTriangleSelectionElements ( const FGeometrySelection& MeshSelection, const UE::Geometry::FDynamicMesh3& Mesh, TFunctionRef< void(int32, const FVector3d&)> VertexFunc, TFunctionRef< void(int32, const FSegment3d&)> EdgeFunc, TFunctionRef< void(int32, const FTriangle3d&)> TriangleFunc, const FTransform* ApplyTransform, const bool bMapFacesToEdgeLoops )

bool UE::Geometry::EnumerateTriangleSelectionElements ( const FGeometrySelection& MeshSelection, const UE::Geometry::FDynamicMesh3& Mesh, TFunctionRef< void(int32, const FVector3d&)> VertexFunc, TFunctionRef< void(int32, const FSegment3d&)> EdgeFunc, TFunctionRef< void(int32, const FTriangle3d&)> TriangleFunc, const FTransform* ApplyTransform, const EEnumerateSelectionMapping Flags )

bool UE::Geometry::EnumerateTriangleSelectionTriangles ( const FGeometrySelection& MeshSelection, const UE::Geometry::FDynamicMesh3& Mesh, TFunctionRef< void(int32)> TriangleFunc )

Please use the function of the same name which takes ApplyTransform as a pointer instead bool UE::Geometry::EnumerateTriangleSelectionVertices ( const FGeometrySelection& MeshSelection, const UE::Geometry::FDynamicMesh3& Mesh, const FTransform& ApplyTransform, TFunctionRef< void(uint64, const FVector3d&)> VertexFunc )

bool UE::Geometry::EnumerateTriangleSelectionVertices ( const FGeometrySelection& MeshSelection, const UE::Geometry::FDynamicMesh3& Mesh, const FTransform* ApplyTransform, TFunctionRef< void(uint64, const FVector3d&)> VertexFunc )

bool UE::Geometry::FindInSelectionByTopologyID ( const FGeometrySelection& GeometrySelection, uint32 TopologyID, uint64& FoundValue )

FDynamicMeshPolygroupAttribute * UE::Geometry::FindPolygroupLayerByName ( FDynamicMesh3& Mesh, FName Name )

const FDynamicMeshPolygroupAttribute * UE::Geometry::FindPolygroupLayerByName ( const FDynamicMesh3& Mesh, FName Name )

int32 UE::Geometry::FindPolygroupLayerIndex ( const FDynamicMesh3& Mesh, const FDynamicMeshPolygroupAttribute* Layer )

int32 UE::Geometry::FindPolygroupLayerIndexByName ( const FDynamicMesh3& Mesh, FName Name )

int32 UE::Geometry::FlipToDelaunay ( FSimpleIntrinsicEdgeFlipMesh& IntrinsicMesh, TSet< int >& Uncorrected, const int32 MaxFlipCount )

int32 UE::Geometry::FlipToDelaunay ( FIntrinsicEdgeFlipMesh& IntrinsicMesh, TSet< int >& Uncorrected, const int32 MaxFlipCount )

int32 UE::Geometry::FlipToDelaunay ( FSimpleIntrinsicMesh& IntrinsicMesh, TSet< int >& Uncorrected, const int32 MaxFlipCount )

int32 UE::Geometry::FlipToDelaunay ( FIntrinsicMesh& IntrinsicMesh, TSet< int >& Uncorrected, const int32 MaxFlipCount )

int32 UE::Geometry::FlipToDelaunay ( FIntrinsicTriangulation& IntrinsicMesh, TSet< int >& Uncorrected, const int32 MaxFlipCount )

FTraceResult UE::Geometry::GeodesicSingleTriangleUtils::TraceFromVertex ( const FDynamicMesh3& Mesh, const FMeshTangentDirection& Direction, double MaxDistance )

FTraceResult UE::Geometry::GeodesicSingleTriangleUtils::TraceFromVertex ( const FDynamicMesh3& Mesh, const FMeshTangentDirection& Direction, FTangentTri2& ScratchTangentTri2, double MaxDistance )

FTraceResult UE::Geometry::GeodesicSingleTriangleUtils::TraceFromVertex ( const FDynamicMesh3& Mesh, int32 VID, const FMeshSurfaceDirection& Direction, double MaxDistance )

FTraceResult UE::Geometry::GeodesicSingleTriangleUtils::TraceFromVertex ( const FDynamicMesh3& Mesh, int32 VID, const FMeshSurfaceDirection& Direction, FTangentTri2& ScratchTangentTri2, double MaxDistance )

FTraceResult UE::Geometry::GeodesicSingleTriangleUtils::TraceNextTriangle ( const FDynamicMesh3& Mesh, const FTraceResult& LastTrace, double MaxDistance )

FTraceResult UE::Geometry::GeodesicSingleTriangleUtils::TraceNextTriangle ( const FDynamicMesh3& Mesh, const FTraceResult& LastTrace, FTangentTri2& ScratchTangentTri2, double MaxDistance )

FTraceResult UE::Geometry::GeodesicSingleTriangleUtils::TraceTangentTriangle ( const FTangentTri2& TangentTri2, const FVector2d& RayOrigin, const FVector2d& RayDir, double MaxDistance )

FTraceResult UE::Geometry::GeodesicSingleTriangleUtils::TraceTriangleFromBaryPoint ( const FDynamicMesh3& Mesh, const int32 TriID, const FVector3d& BaryPoint, const FMeshSurfaceDirection& Direction, double MaxDistance )

FTraceResult UE::Geometry::GeodesicSingleTriangleUtils::TraceTriangleFromBaryPoint ( const FDynamicMesh3& Mesh, const int32 TriID, const FVector3d& BaryPoint, const FMeshSurfaceDirection& Direction, FTangentTri2& ScratchTangentTri2, double MaxDistance )

FTraceResult UE::Geometry::GeodesicSingleTriangleUtils::TraceTriangleFromEdge ( const FDynamicMesh3& Mesh, const int32 TriID, double EdgeAlpha, const FMeshSurfaceDirection& Direction, double MaxDistance )

FTraceResult UE::Geometry::GeodesicSingleTriangleUtils::TraceTriangleFromEdge ( const FDynamicMesh3& Mesh, const int32 TriID, double EdgeAlpha, const FMeshSurfaceDirection& Direction, FTangentTri2& ScratchTangentTri2, double MaxDistance )

const void * UE::Geometry::GetDetailMeshTrianglePoint_Nearest ( const IMeshBakerDetailSampler* DetailSpatial, const FVector3d& BasePoint, int32& DetailTriangleOut, FVector3d& DetailTriBaryCoords )

const void * UE::Geometry::GetDetailMeshTrianglePoint_Raycast ( const IMeshBakerDetailSampler* DetailSpatial, const FVector3d& BasePoint, const FVector3d& BaseNormal, int32& DetailTriangleOut, FVector3d& DetailTriBaryCoords, double Thickness, bool bFailToNearestPoint )

bool UE::Geometry::GetSelectionBoundaryCorners ( const UE::Geometry::FDynamicMesh3& Mesh, const UE::Geometry::FGroupTopology* GroupTopology, const UE::Geometry::FGeometrySelection& ReferenceSelection, TSet< int32 >& BorderCornerIDsOut, TSet< int32 >& CurCornerIDsOut )

bool UE::Geometry::GetSelectionBoundaryVertices ( const UE::Geometry::FDynamicMesh3& Mesh, const UE::Geometry::FGroupTopology* GroupTopology, const UE::Geometry::FGeometrySelection& ReferenceSelection, TSet< int32 >& BorderVidsOut, TSet< int32 >& CurVerticesOut )

bool UE::Geometry::GetTriangleSelectionFrame ( const FGeometrySelection& MeshSelection, const UE::Geometry::FDynamicMesh3& Mesh, FFrame3d& SelectionFrameOut )

bool UE::Geometry::InitializeSelectionFromTriangles ( const UE::Geometry::FDynamicMesh3& Mesh, const FGroupTopology* GroupTopology, TArrayView< const int > Triangles, FGeometrySelection& SelectionOut )

FVector3d UE::Geometry::IntrinsicCorrespondenceUtils::AsR3Position ( const FSurfacePoint& SurfacePoint, const FDynamicMesh3& Mesh, bool& bValidPoint )

bool UE::Geometry::IntrinsicCorrespondenceUtils::VisitVertexAdjacentElements ( const MeshType& Mesh, const int32 VID, const int32 StartEID, FunctorType& Functor )

bool UE::Geometry::IsBoxMesh ( const FDynamicMesh3& Mesh, FOrientedBox3d& BoxOut, double AngleToleranceDeg, double PlaneDistanceTolerance )

bool UE::Geometry::IsCapsuleMesh ( const FDynamicMesh3& Mesh, FCapsule3d& CapsuleOut, double RelativeDeviationTol, double MaxAngleRangeDegrees )

bool UE::Geometry::IsSphereMesh ( const FDynamicMesh3& Mesh, FSphere3d& SphereOut, double RelativeDeviationTol, double MaxAngleRangeDegrees )

bool UE::Geometry::MakeBoundaryConnectedSelection ( const UE::Geometry::FDynamicMesh3& Mesh, const FGroupTopology* GroupTopology, const FGeometrySelection& ReferenceSelection, TFunctionRef< bool(FGeoSelectionID)> SelectionIDPredicate, FGeometrySelection& BoundaryConnectedSelection )

bool UE::Geometry::MakeSelectAllConnectedSelection ( const UE::Geometry::FDynamicMesh3& Mesh, const FGroupTopology* GroupTopology, const FGeometrySelection& ReferenceSelection, TFunctionRef< bool(FGeoSelectionID)> SelectionIDPredicate, TFunctionRef< bool(FGeoSelectionIDA, FGeoSelectionIDB)> IsConnectedPredicate, FGeometrySelection& AllConnectedSelection )

bool UE::Geometry::MakeSelectAllSelection ( const UE::Geometry::FDynamicMesh3& Mesh, const FGroupTopology* GroupTopology, TFunctionRef< bool(FGeoSelectionID)> SelectionIDPredicate, FGeometrySelection& AllSelection )

FString UE::Geometry::MakeUniqueGroupLayerName ( const FDynamicMesh3& Mesh, FString BaseName )

bool UE::Geometry::operator! ( EOcclusionMapType E )

bool UE::Geometry::operator! ( EMeshOcclusionMapType E )

bool UE::Geometry::operator! ( EEnumerateSelectionMapping E )

bool UE::Geometry::operator! ( ESimpleShapeType E )

EOcclusionMapType UE::Geometry::operator& ( EOcclusionMapType Lhs, EOcclusionMapType Rhs )

EMeshOcclusionMapType UE::Geometry::operator& ( EMeshOcclusionMapType Lhs, EMeshOcclusionMapType Rhs )

EEnumerateSelectionMapping UE::Geometry::operator& ( EEnumerateSelectionMapping Lhs, EEnumerateSelectionMapping Rhs )

ESimpleShapeType UE::Geometry::operator& ( ESimpleShapeType Lhs, ESimpleShapeType Rhs )

EOcclusionMapType & UE::Geometry::operator&= ( EOcclusionMapType& Lhs, EOcclusionMapType Rhs )

EMeshOcclusionMapType & UE::Geometry::operator&= ( EMeshOcclusionMapType& Lhs, EMeshOcclusionMapType Rhs )

EEnumerateSelectionMapping & UE::Geometry::operator&= ( EEnumerateSelectionMapping& Lhs, EEnumerateSelectionMapping Rhs )

ESimpleShapeType & UE::Geometry::operator&= ( ESimpleShapeType& Lhs, ESimpleShapeType Rhs )

EOcclusionMapType UE::Geometry::operator^ ( EOcclusionMapType Lhs, EOcclusionMapType Rhs )

EMeshOcclusionMapType UE::Geometry::operator^ ( EMeshOcclusionMapType Lhs, EMeshOcclusionMapType Rhs )

EEnumerateSelectionMapping UE::Geometry::operator^ ( EEnumerateSelectionMapping Lhs, EEnumerateSelectionMapping Rhs )

ESimpleShapeType UE::Geometry::operator^ ( ESimpleShapeType Lhs, ESimpleShapeType Rhs )

EOcclusionMapType & UE::Geometry::operator^= ( EOcclusionMapType& Lhs, EOcclusionMapType Rhs )

EMeshOcclusionMapType & UE::Geometry::operator^= ( EMeshOcclusionMapType& Lhs, EMeshOcclusionMapType Rhs )

EEnumerateSelectionMapping & UE::Geometry::operator^= ( EEnumerateSelectionMapping& Lhs, EEnumerateSelectionMapping Rhs )

ESimpleShapeType & UE::Geometry::operator^= ( ESimpleShapeType& Lhs, ESimpleShapeType Rhs )

EOcclusionMapType UE::Geometry::operator| ( EOcclusionMapType Lhs, EOcclusionMapType Rhs )

EMeshOcclusionMapType UE::Geometry::operator| ( EMeshOcclusionMapType Lhs, EMeshOcclusionMapType Rhs )

EEnumerateSelectionMapping UE::Geometry::operator| ( EEnumerateSelectionMapping Lhs, EEnumerateSelectionMapping Rhs )

ESimpleShapeType UE::Geometry::operator| ( ESimpleShapeType Lhs, ESimpleShapeType Rhs )

EOcclusionMapType & UE::Geometry::operator|= ( EOcclusionMapType& Lhs, EOcclusionMapType Rhs )

EMeshOcclusionMapType & UE::Geometry::operator|= ( EMeshOcclusionMapType& Lhs, EMeshOcclusionMapType Rhs )

EEnumerateSelectionMapping & UE::Geometry::operator|= ( EEnumerateSelectionMapping& Lhs, EEnumerateSelectionMapping Rhs )

ESimpleShapeType & UE::Geometry::operator|= ( ESimpleShapeType& Lhs, ESimpleShapeType Rhs )

EOcclusionMapType UE::Geometry::operator~ ( EOcclusionMapType E )

EMeshOcclusionMapType UE::Geometry::operator~ ( EMeshOcclusionMapType E )

EEnumerateSelectionMapping UE::Geometry::operator~ ( EEnumerateSelectionMapping E )

ESimpleShapeType UE::Geometry::operator~ ( ESimpleShapeType E )

FVector3d UE::Geometry::SolveInsetVertexPositionFromLinePair ( const FVector3d& Position, const FLine3d& InsetEdgeLine1, const FLine3d& InsetEdgeLine2 )

void UE::Geometry::SolveInsetVertexPositionsFromInsetLines ( const FDynamicMesh3& Mesh, const TArray< FLine3d >& InsetEdgeLines, const TArray< int32 >& VertexIDs, TArray< FVector3d >& VertexPositionsOut, bool bIsLoop )

double UE::Geometry::SumPathLength ( const FDeformableEdgePath& DeformableEdgePath )

void UE::Geometry::TaperPerTriangleValues ( const UE::Geometry::FDynamicMesh3& Mesh, const TSet< int32 >& TriangleROI, TFunction< int32(int32)> ValueForTriangleFunc, TArray< int >& OutTriangleValues )

void UE::Geometry::UpdateGroupSelectionViaRaycast ( const FColliderMesh* ColliderMesh, const FGroupTopology* GroupTopology, FGeometrySelectionEditor* Editor, const FRay3d& LocalRay, const FGeometrySelectionUpdateConfig& UpdateConfig, FGeometrySelectionUpdateResult& ResultOut )

bool UE::Geometry::UpdateSelectionWithNewElements ( FGeometrySelectionEditor* Editor, EGeometrySelectionChangeType ChangeType, const TArray< uint64 >& NewIDs, FGeometrySelectionDelta* DeltaOut )

void UE::Geometry::UpdateTriangleSelectionViaRaycast ( const FColliderMesh* ColliderMesh, FGeometrySelectionEditor* Editor, const FRay3d& LocalRay, const FGeometrySelectionUpdateConfig& UpdateConfig, FGeometrySelectionUpdateResult& ResultOut )

bool UE::Geometry::UVUnwrapMeshUtil::DoesUnwrapMatchOverlay ( const FDynamicMeshUVOverlay& OverlayIn, const FDynamicMesh3& UnwrapMeshIn, TFunctionRef< FVector3d(const FVector2f&)> UVToVertPosition, double Tolerance )

void UE::Geometry::UVUnwrapMeshUtil::GenerateUVUnwrapMesh ( const FDynamicMeshUVOverlay& UVOverlay, FDynamicMesh3& UnwrapMeshOut, TFunctionRef< FVector3d(const FVector2f&)> UVToVertPosition )

void UE::Geometry::UVUnwrapMeshUtil::UpdateOverlayFromOverlay ( const FDynamicMeshUVOverlay& OverlayIn, FDynamicMeshUVOverlay& OverlayOut, bool bParentVertsIdentical, const TArray< int32 >* ChangedElements, const TArray< int32 >* ChangedConnectivityTids )

void UE::Geometry::UVUnwrapMeshUtil::UpdateUVOverlayFromUnwrapMesh ( const FDynamicMesh3& UnwrapMeshIn, FDynamicMeshUVOverlay& UVOverlayOut, TFunctionRef< FVector2f(const FVector3d&)> VertPositionToUV, const TArray< int32 >* ChangedVids, const TArray< int32 >* ChangedConnectivityTids )

void UE::Geometry::UVUnwrapMeshUtil::UpdateUVUnwrapMesh ( const FDynamicMesh3& SourceUnwrapMesh, FDynamicMesh3& DestUnwrapMesh, const TArray< int32 >* ChangedVids, const TArray< int32 >* ChangedConnectivityTids )

void UE::Geometry::UVUnwrapMeshUtil::UpdateUVUnwrapMesh ( const FDynamicMeshUVOverlay& UVOverlayIn, FDynamicMesh3& UnwrapMeshOut, TFunctionRef< FVector3d(const FVector2f&)> UVToVertPosition, const TArray< int32 >* ChangedElementIDs, const TArray< int32 >* ChangedConnectivityTids )

double UE::MeshCurvature::GaussianCurvature ( const FDynamicMesh3& Mesh, int32 VertexIndex )

double UE::MeshCurvature::GaussianCurvature ( const FDynamicMesh3& Mesh, int32 VertexIndex, TFunctionRef< FVector3d(int32)> VertexPositionFunc )

FVector3d UE::MeshCurvature::MeanCurvatureNormal ( const FDynamicMesh3& Mesh, int32 VertexIndex )

FVector3d UE::MeshCurvature::MeanCurvatureNormal ( const FDynamicMesh3& Mesh, int32 VertexIndex, TFunctionRef< FVector3d(int32)> VertexPositionFunc )

int32 UE::MeshDeformation::ComputeNumMatrixElements ( const MeshT& DynamicMesh, const TArray< int32 >& ToVtxId )

void UE::MeshDeformation::ComputeSmoothing_BiHarmonic ( const ELaplacianWeightScheme WeightingScheme, const FDynamicMesh3& OriginalMesh, const double Speed, const double Weight, const int32 NumIterations, TArray< FVector3d >& PositionArray, FProgressCancel* Progress )

void UE::MeshDeformation::ComputeSmoothing_Diffusion ( const ELaplacianWeightScheme WeightScheme, const FDynamicMesh3& OriginalMesh, bool bForwardEuler, const double Speed, double Weight, const int32 NumIterations, TArray< FVector3d >& PositionArray, FProgressCancel* Progress )

void UE::MeshDeformation::ComputeSmoothing_Forward ( bool bUniformWeightScheme, bool bSmoothBoundary, const FDynamicMesh3& OriginalMesh, TFunctionRef< double(int VID, bool bBoundary)> GetSmoothingAlpha, const int32 NumIterations, TArray< FVector3d >& PositionArray, FProgressCancel* Progress )

void UE::MeshDeformation::ComputeSmoothing_ImplicitBiHarmonicPCG ( const ELaplacianWeightScheme WeightScheme, const FDynamicMesh3& OriginalMesh, const double Speed, const double Weight, const int32 MaxIterations, TArray< FVector3d >& PositionArray )

TUniquePtr< UE::Solvers::IConstrainedMeshSolver > UE::MeshDeformation::ConstructConstrainedMeshDeformer ( const ELaplacianWeightScheme WeightScheme, const FDynamicMesh3& DynamicMesh )

TUniquePtr< UE::Solvers::IConstrainedMeshSolver > UE::MeshDeformation::ConstructConstrainedMeshSmoother ( const ELaplacianWeightScheme WeightScheme, const FDynamicMesh3& DynamicMesh )

void UE::MeshDeformation::ConstructCotangentLaplacian ( const FDynamicMesh3& DynamicMesh, const FVertexLinearization& VertexMap, UE::Solvers::TSparseMatrixAssembler< RealType >& AreaMatrix, UE::Solvers::TSparseMatrixAssembler< RealType >& LaplacianInterior, UE::Solvers::TSparseMatrixAssembler< RealType >& LaplacianBoundary )

void UE::MeshDeformation::ConstructCotangentLaplacian ( const FDynamicMesh3& DynamicMesh, const FVertexLinearization& VertexMap, UE::Solvers::TSparseMatrixAssembler< RealType >& LaplacianInterior, UE::Solvers::TSparseMatrixAssembler< RealType >& LaplacianBoundary, const bool bClampWeights )

void UE::MeshDeformation::ConstructEdgeCotanWeightsDataArray ( const FDynamicMesh3& Mesh, TArray< double >& EdgeWeightsDataArray, double ClampMin, double ClampMax )

void UE::MeshDeformation::ConstructFullCotangentLaplacian ( const FDynamicMesh3& DynamicMesh, const FVertexLinearization& VertexMap, UE::Solvers::TSparseMatrixAssembler< RealType >& LaplacianMatrix, ECotangentWeightMode WeightMode, ECotangentAreaMode AreaMode )

void UE::MeshDeformation::ConstructFullIDTCotangentLaplacian ( const FDynamicMesh3& Mesh, const FVertexLinearization& VertexMap, UE::Solvers::TSparseMatrixAssembler< RealType >& LaplacianMatrix, ECotangentWeightMode WeightMode, ECotangentAreaMode AreaMode )

void UE::MeshDeformation::ConstructIDTCotangentLaplacian ( const FDynamicMesh3& DynamicMesh, const FVertexLinearization& VertexMap, UE::Solvers::TSparseMatrixAssembler< RealType >& LaplacianInterior, UE::Solvers::TSparseMatrixAssembler< RealType >& LaplacianBoundary, const bool bClampWeights )

void UE::MeshDeformation::ConstructMeanValueWeightLaplacian ( const FDynamicMesh3& DynamicMesh, const FVertexLinearization& VertexMap, UE::Solvers::TSparseMatrixAssembler< RealType >& LaplacianInterior, UE::Solvers::TSparseMatrixAssembler< RealType >& LaplacianBoundary )

TUniquePtr< UE::Solvers::IConstrainedMeshUVSolver > UE::MeshDeformation::ConstructNaturalConformalParamSolver ( const FDynamicMesh3& DynamicMesh )

TUniquePtr< UE::Solvers::IConstrainedLaplacianMeshSolver > UE::MeshDeformation::ConstructSoftMeshDeformer ( const FDynamicMesh3& DynamicMesh )

TUniquePtr< UE::Solvers::IConstrainedMeshUVSolver > UE::MeshDeformation::ConstructSpectralConformalParamSolver ( const FDynamicMesh3& DynamicMesh, bool bPreserveIrregularity )

void UE::MeshDeformation::ConstructTriangleDataArray ( const FDynamicMesh3& DynamicMesh, const FTriangleLinearization& TriangleLinearization, TArray< TriangleDataType >& TriangleDataArray )

void UE::MeshDeformation::ConstructUmbrellaLaplacian ( const FDynamicMesh3& DynamicMesh, const FVertexLinearization& VertexMap, UE::Solvers::TSparseMatrixAssembler< RealType >& LaplacianInterior, UE::Solvers::TSparseMatrixAssembler< RealType >& LaplacianBoundary )

TUniquePtr< UE::Solvers::IConstrainedMeshSolver > UE::MeshDeformation::ConstructUniformConstrainedMeshDeformer ( const FDynamicGraph3d& Graph )

void UE::MeshDeformation::ConstructUniformLaplacian ( const MeshType& Mesh, const FVertexLinearization& VertexMap, UE::Solvers::TSparseMatrixAssembler< RealType >& LaplacianInterior, UE::Solvers::TSparseMatrixAssembler< RealType >& LaplacianBoundary )

void UE::MeshDeformation::ConstructValenceWeightedLaplacian ( const FDynamicMesh3& DynamicMesh, const FVertexLinearization& VertexMap, UE::Solvers::TSparseMatrixAssembler< RealType >& LaplacianInterior, UE::Solvers::TSparseMatrixAssembler< RealType >& LaplacianBoundary )

void UE::MeshUVTransforms::FitToBox ( FDynamicMeshUVOverlay* UVOverlay, const FAxisAlignedBox2d& Box, bool bUniformScale )

void UE::MeshUVTransforms::FitToBox ( FDynamicMeshUVOverlay* UVOverlay, const TArray< int32 >& UVElementIDs, const FAxisAlignedBox2d& Box, bool bUniformScale )

void UE::MeshUVTransforms::MakeSeamsDisjoint ( FDynamicMeshUVOverlay* UVOverlay )

void UE::MeshUVTransforms::RecenterScale ( FDynamicMeshUVOverlay* UVOverlay, const TArray< int32 >& UVElementIDs, EIslandPositionType NewPosition, double UVScale )

static double UE::Geometry::AsZeroToTwoPi ( double AngleR )

static bool UE::Geometry::GeodesicSingleTriangleUtils::IsTerminated ( const FTraceResult& Result )

static bool UE::Geometry::IntrinsicCorrespondenceUtils::IsEdgePoint ( const FSurfacePoint& SurfacePoint )

static bool UE::Geometry::IntrinsicCorrespondenceUtils::IsFacePoint ( const FSurfacePoint& SurfacePoint )

static bool UE::Geometry::IntrinsicCorrespondenceUtils::IsVertexPoint ( const FSurfacePoint& SurfacePoint )



---

## DynamicWindEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DynamicWindEditor

**Contents:**
- DynamicWindEditor
- Navigation
- Classes
- Structs



---

## DynamicWind

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/DynamicWind

**Contents:**
- DynamicWind
- Navigation
- Classes
- Structs



---

## EaseCurveTool

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/EaseCurveTool

**Contents:**
- EaseCurveTool
- Navigation
- Classes



---

## EditorDebugTools

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/EditorDebugTools

**Contents:**
- EditorDebugTools
- Navigation
- Classes



---

## EditorPerformance

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/EditorPerformance

**Contents:**
- EditorPerformance
- Navigation
- Classes
- Typedefs



---

## EditorScriptableToolsFramework

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/EditorScriptableToolsFramework

**Contents:**
- EditorScriptableToolsFramework
- Navigation
- Classes
- Typedefs



---

## EditorScriptingUtilities

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/EditorScriptingUtilities

**Contents:**
- EditorScriptingUtilities
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## EditorSysConfigAssistant

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/EditorSysConfigAssistant

**Contents:**
- EditorSysConfigAssistant
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

bool operator! ( EEditorSysConfigFeatureRemediationFlags E )

EEditorSysConfigFeatureRemediationFlags operator& ( EEditorSysConfigFeatureRemediationFlags Lhs, EEditorSysConfigFeatureRemediationFlags Rhs )

EEditorSysConfigFeatureRemediationFlags & operator&= ( EEditorSysConfigFeatureRemediationFlags& Lhs, EEditorSysConfigFeatureRemediationFlags Rhs )

EEditorSysConfigFeatureRemediationFlags operator^ ( EEditorSysConfigFeatureRemediationFlags Lhs, EEditorSysConfigFeatureRemediationFlags Rhs )

EEditorSysConfigFeatureRemediationFlags & operator^= ( EEditorSysConfigFeatureRemediationFlags& Lhs, EEditorSysConfigFeatureRemediationFlags Rhs )

EEditorSysConfigFeatureRemediationFlags operator| ( EEditorSysConfigFeatureRemediationFlags Lhs, EEditorSysConfigFeatureRemediationFlags Rhs )

EEditorSysConfigFeatureRemediationFlags & operator|= ( EEditorSysConfigFeatureRemediationFlags& Lhs, EEditorSysConfigFeatureRemediationFlags Rhs )

EEditorSysConfigFeatureRemediationFlags operator~ ( EEditorSysConfigFeatureRemediationFlags E )



---

## EditorTelemetry

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/EditorTelemetry

**Contents:**
- EditorTelemetry
- Navigation
- Classes



---

## EditorTests

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/EditorTests

**Contents:**
- EditorTests
- Navigation
- Classes
- Enums
  - Public



---

## EditorTraceUtilities

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/EditorTraceUtilities

**Contents:**
- EditorTraceUtilities
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## ElectraBase

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ElectraBase

**Contents:**
- ElectraBase
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Functions
  - Public
  - Static

T Electra::AdvancePointer ( T pPointer, C numBytes )

void Electra::LexFromStringHex ( int32& OutValue, const TCHAR* Buffer )

void Electra::LexFromStringHex64 ( int64& OutValue, const TCHAR* Buffer )

void Electra::LexFromStringHexU64 ( uint64& OutValue, const TCHAR* Buffer )

TSharedRef< T, ESPMode::ThreadSafe > Electra::MakeSharedTS ( ArgTypes&&... Args )

T Electra::Utils::AbsoluteValue ( T Value )

uint32 Electra::Utils::BitReverse32 ( uint32 InValue )

uint16 Electra::Utils::EndianSwap ( uint16 value )

int16 Electra::Utils::EndianSwap ( int16 value )

uint32 Electra::Utils::EndianSwap ( uint32 value )

int32 Electra::Utils::EndianSwap ( int32 value )

uint64 Electra::Utils::EndianSwap ( uint64 value )

int64 Electra::Utils::EndianSwap ( int64 value )

uint32 Electra::Utils::Make4CC ( const uint8 A, const uint8 B, const uint8 C, const uint8 D )

T Electra::Utils::Max ( T a, T b )

T Electra::Utils::Min ( T a, T b )

uint32 FMediaInterlockedAdd ( uint32 volatile& variable, uint32 value )

int32 FMediaInterlockedAdd ( int32 volatile& variable, int32 value )

uint64 FMediaInterlockedAdd64 ( uint64 volatile& variable, uint64 value )

uint32 FMediaInterlockedCompareExchange ( uint32 volatile& variable, uint32 exchangeValue, uint32 compareValue )

int32 FMediaInterlockedCompareExchange ( int32 volatile& variable, int32 exchangeValue, int32 compareValue )

void * FMediaInterlockedCompareExchangePointer ( void*volatile& variable, void* pExchangeValue, void* pCompareValue )

uint32 FMediaInterlockedDecrement ( uint32 volatile& variable )

int32 FMediaInterlockedDecrement ( int32 volatile& variable )

uint32 FMediaInterlockedExchange ( uint32 volatile& variable, uint32 exchangeValue )

int32 FMediaInterlockedExchange ( int32 volatile& variable, int32 exchangeValue )

void * FMediaInterlockedExchangePointerVoid ( void*volatile& variable, void* pExchangeValue )

uint32 FMediaInterlockedIncrement ( uint32 volatile& variable )

int32 FMediaInterlockedIncrement ( int32 volatile& variable )

uint32 FMediaInterlockedRead ( uint32 volatile& variable )

int32 FMediaInterlockedRead ( int32 volatile& variable )

uint64 FMediaInterlockedRead64 ( uint64 volatile& variable )

T * TMediaInterlockedExchangePointer ( T*volatile& variable, X* pExchangeValue )

static uint8 Electra::GetFromBigEndian ( uint8 value )

static int8 Electra::GetFromBigEndian ( int8 value )

static uint16 Electra::GetFromBigEndian ( uint16 value )

static int16 Electra::GetFromBigEndian ( int16 value )

static int32 Electra::GetFromBigEndian ( int32 value )

static uint32 Electra::GetFromBigEndian ( uint32 value )

static int64 Electra::GetFromBigEndian ( int64 value )

static uint64 Electra::GetFromBigEndian ( uint64 value )

static FString Electra::UtilitiesMP4::GetPrintableBoxAtom ( uint32 InAtom )

static uint32 Electra::UtilitiesMP4::MakeBoxAtom ( const uint8 A, const uint8 B, const uint8 C, const uint8 D )

static FString Electra::UtilitiesMP4::Printable4CC ( const uint32 In4CC )

static const FName IDecoderOutputOptionNames::AspectH ( TEXT("aspect_h") )

static const FName IDecoderOutputOptionNames::AspectRatio ( TEXT("aspect_ratio") )

static const FName IDecoderOutputOptionNames::AspectW ( TEXT("aspect_w") )

static const FName IDecoderOutputOptionNames::BitsPerComponent ( TEXT("bits_per") )

static const FName IDecoderOutputOptionNames::Colorimetry ( TEXT("colorimetry") )

static const FName IDecoderOutputOptionNames::CropBottom ( TEXT("crop_bottom") )

static const FName IDecoderOutputOptionNames::CropLeft ( TEXT("crop_left") )

static const FName IDecoderOutputOptionNames::CropRight ( TEXT("crop_right") )

static const FName IDecoderOutputOptionNames::CropTop ( TEXT("crop_top") )

static const FName IDecoderOutputOptionNames::Duration ( TEXT("duration") )

static const FName IDecoderOutputOptionNames::FPSDenominator ( TEXT("fps_denom") )

static const FName IDecoderOutputOptionNames::FPSNumerator ( TEXT("fps_num") )

static const FName IDecoderOutputOptionNames::HDRInfo ( TEXT("hdr_info") )

static const FName IDecoderOutputOptionNames::Height ( TEXT("height") )

static const FName IDecoderOutputOptionNames::Orientation ( TEXT("orientation") )

static const FName IDecoderOutputOptionNames::Pitch ( TEXT("pitch") )

static const FName IDecoderOutputOptionNames::PixelDataScale ( TEXT("pix_datascale") )

static const FName IDecoderOutputOptionNames::PixelEncoding ( TEXT("pixelenc") )

static const FName IDecoderOutputOptionNames::PixelFormat ( TEXT("pixelfmt") )

static const FName IDecoderOutputOptionNames::PTS ( TEXT("pts") )

static const FName IDecoderOutputOptionNames::Timecode ( TEXT("timecode") )

static const FName IDecoderOutputOptionNames::TMCDFramerate ( TEXT("tmcd_framerate") )

static const FName IDecoderOutputOptionNames::TMCDTimecode ( TEXT("tmcd_timecode") )

static const FName IDecoderOutputOptionNames::Width ( TEXT("width") )

static uint16 MEDIA_ENDIAN_SWAP ( uint16 value )

static int16 MEDIA_ENDIAN_SWAP ( int16 value )

static uint32 MEDIA_ENDIAN_SWAP ( uint32 value )

static int32 MEDIA_ENDIAN_SWAP ( int32 value )

static uint64 MEDIA_ENDIAN_SWAP ( uint64 value )

static int64 MEDIA_ENDIAN_SWAP ( int64 value )

static uint8 MEDIA_FROM_BIG_ENDIAN ( uint8 value )

static int8 MEDIA_FROM_BIG_ENDIAN ( int8 value )

static uint16 MEDIA_FROM_BIG_ENDIAN ( uint16 value )

static int16 MEDIA_FROM_BIG_ENDIAN ( int16 value )

static int32 MEDIA_FROM_BIG_ENDIAN ( int32 value )

static uint32 MEDIA_FROM_BIG_ENDIAN ( uint32 value )

static int64 MEDIA_FROM_BIG_ENDIAN ( int64 value )

static uint64 MEDIA_FROM_BIG_ENDIAN ( uint64 value )

static uint8 MEDIA_FROM_LITTLE_ENDIAN ( uint8 value )

static int8 MEDIA_FROM_LITTLE_ENDIAN ( int8 value )

static uint16 MEDIA_FROM_LITTLE_ENDIAN ( uint16 value )

static int16 MEDIA_FROM_LITTLE_ENDIAN ( int16 value )

static int32 MEDIA_FROM_LITTLE_ENDIAN ( int32 value )

static uint32 MEDIA_FROM_LITTLE_ENDIAN ( uint32 value )

static int64 MEDIA_FROM_LITTLE_ENDIAN ( int64 value )

static uint64 MEDIA_FROM_LITTLE_ENDIAN ( uint64 value )

static uint8 MEDIA_TO_BIG_ENDIAN ( uint8 value )

static int8 MEDIA_TO_BIG_ENDIAN ( int8 value )

static uint16 MEDIA_TO_BIG_ENDIAN ( uint16 value )

static int16 MEDIA_TO_BIG_ENDIAN ( int16 value )

static int32 MEDIA_TO_BIG_ENDIAN ( int32 value )

static uint32 MEDIA_TO_BIG_ENDIAN ( uint32 value )

static int64 MEDIA_TO_BIG_ENDIAN ( int64 value )

static uint64 MEDIA_TO_BIG_ENDIAN ( uint64 value )

static uint8 MEDIA_TO_LITTLE_ENDIAN ( uint8 value )

static int8 MEDIA_TO_LITTLE_ENDIAN ( int8 value )

static uint16 MEDIA_TO_LITTLE_ENDIAN ( uint16 value )

static int16 MEDIA_TO_LITTLE_ENDIAN ( int16 value )

static int32 MEDIA_TO_LITTLE_ENDIAN ( int32 value )

static uint32 MEDIA_TO_LITTLE_ENDIAN ( uint32 value )

static int64 MEDIA_TO_LITTLE_ENDIAN ( int64 value )

static uint64 MEDIA_TO_LITTLE_ENDIAN ( uint64 value )



---

## ElectraCDM

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ElectraCDM

**Contents:**
- ElectraCDM
- Navigation
- Structs
- Interfaces
- Enums
  - Public



---

## ElectraCodecFactory

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ElectraCodecFactory

**Contents:**
- ElectraCodecFactory
- Navigation
- Interfaces



---

## ElectraDecoders

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ElectraDecoders

**Contents:**
- ElectraDecoders
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

Colorimetry information in standard MPEG definition. | IElectraDecoderFeaturesAndOptions.h | |

Timing from a bitstream SEI message. | IElectraDecoderFeaturesAndOptions.h | |

A human readable string of the format to be decoded. | IElectraDecoderFeaturesAndOptions.h | |

Number of luminance bits. | IElectraDecoderFeaturesAndOptions.h | |

Content light level info from bitstream SEI message | IElectraDecoderFeaturesAndOptions.h | |

T ElectraDecodersUtil::AbsoluteValue ( T Value )

T ElectraDecodersUtil::AdvancePointer ( T pPointer, C numBytes )

uint32 ElectraDecodersUtil::BitReverse32 ( uint32 InValue )

T ElectraDecodersUtil::Max ( T a, T b )

T ElectraDecodersUtil::Min ( T a, T b )

bool ElectraDecodersUtil::MPEG::H264::ParseSequenceParameterSet ( FSequenceParameterSet& OutSequenceParameterSet, const TArray< uint8 >& InData )

bool ElectraDecodersUtil::MPEG::H265::ParseSequenceParameterSet ( FSequenceParameterSet& OutSequenceParameterSet, const TArray< uint8 >& InData )

bool ElectraDecodersUtil::MPEG::H265::ParseVideoParameterSet ( FVideoParameterSet& OutSequenceParameterSet, const TArray< uint8 >& InData )

ENUM_CLASS_FLAGS ( EElectraDecoderFlags )

static uint32 ElectraDecodersUtil::Make4CC ( const uint8 A, const uint8 B, const uint8 C, const uint8 D )



---

## ElectraHTTPStream

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ElectraHTTPStream

**Contents:**
- ElectraHTTPStream
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## ElectraPlayerPluginHandler

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ElectraPlayerPluginHandler

**Contents:**
- ElectraPlayerPluginHandler
- Navigation
- Classes



---

## ElectraPlayerPlugin

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ElectraPlayerPlugin

**Contents:**
- ElectraPlayerPlugin
- Navigation
- Interfaces



---

## ElectraPlayerRuntime

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ElectraPlayerRuntime

**Contents:**
- ElectraPlayerRuntime
- Navigation
- Classes
- Interfaces
- Variables
  - Public
- Functions
  - Public

CSV_DECLARE_CATEGORY_MODULE_EXTERN ( ELECTRAPLAYERRUNTIME_API, MediaStreaming )

CSV_DECLARE_CATEGORY_MODULE_EXTERN ( ELECTRAPLAYERRUNTIME_API, ElectraPlayer )

DECLARE_TS_MULTICAST_DELEGATE_FourParams ( FElectraPlayerReportSubtitlesMetricsDelegate, const FGuid&, const FString&, double, const FString& )

DECLARE_TS_MULTICAST_DELEGATE_OneParam ( FElectraPlayerSendAnalyticMetricsPerMinuteDelegate, const TSharedPtr< IAnalyticsProviderET >& )

DECLARE_TS_MULTICAST_DELEGATE_TwoParams ( FElectraPlayerSendAnalyticMetricsDelegate, const TSharedPtr< IAnalyticsProviderET >&, const FGuid& )

DECLARE_TS_MULTICAST_DELEGATE_TwoParams ( FElectraPlayerReportVideoStreamingErrorDelegate, const FGuid&, const FString& )



---

## ElectraProtron

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ElectraProtron

**Contents:**
- ElectraProtron
- Navigation
- Interfaces



---

## ElectraSamples

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ElectraSamples

**Contents:**
- ElectraSamples
- Navigation
- Classes
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Functions
  - Public

UE::Color::EColorSpace ElectraColorimetryUtils::TranslateMPEGColorPrimaries ( uint8 InPrimaries )

UE::Color::EColorSpace ElectraColorimetryUtils::TranslateMPEGMatrixCoefficients ( uint8 InMatrixCoefficients )

UE::Color::EEncoding ElectraColorimetryUtils::TranslateMPEGTransferCharacteristics ( uint8 InTransferCharacteristics )



---

## ElectraSubtitles

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ElectraSubtitles

**Contents:**
- ElectraSubtitles
- Navigation
- Interfaces



---

## EngineAssetDefinitions

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/EngineAssetDefinitions

**Contents:**
- EngineAssetDefinitions
- Navigation
- Classes



---

## EngineCameras

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/EngineCameras

**Contents:**
- EngineCameras
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## EnhancedInput

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/EnhancedInput

**Contents:**
- EnhancedInput
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

ENUM_CLASS_FLAGS ( EMappingQueryIssue )

ENUM_RANGE_BY_FIRST_AND_LAST ( EPlayerMappableKeySlot, EPlayerMappableKeySlot::First, EPlayerMappableKeySlot::Seventh )

UE::EnhancedInput::UE_DECLARE_GAMEPLAY_TAG_EXTERN ( InputMode_Default )



---

## EnvironmentQueryEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/EnvironmentQueryEditor

**Contents:**
- EnvironmentQueryEditor
- Navigation
- Classes
- Structs
- Interfaces



---

## EOSShared

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/EOSShared

**Contents:**
- EOSShared
- Navigation
- Classes



---

## EOSVoiceChat

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/EOSVoiceChat

**Contents:**
- EOSVoiceChat
- Navigation
- Structs



---

## EpicStageApp

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/EpicStageApp

**Contents:**
- EpicStageApp
- Navigation
- Classes
- Structs



---

## EvaluationNotifiesEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/EvaluationNotifiesEditor

**Contents:**
- EvaluationNotifiesEditor
- Navigation
- Classes
- Interfaces



---

## EvaluationNotifiesRuntime

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/EvaluationNotifiesRuntime

**Contents:**
- EvaluationNotifiesRuntime
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## ExampleCharacterFXEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ExampleCharacterFXEditor

**Contents:**
- ExampleCharacterFXEditor
- Navigation
- Classes



---

## ExampleCustomDataInterface

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ExampleCustomDataInterface

**Contents:**
- ExampleCustomDataInterface
- Navigation
- Classes



---

## ExampleDeviceProfileSelector

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ExampleDeviceProfileSelector

**Contents:**
- ExampleDeviceProfileSelector
- Navigation



---

## ExrReaderGpu

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ExrReaderGpu

**Contents:**
- ExrReaderGpu
- Navigation
- Classes



---

## ExternalGPUStatistics

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ExternalGPUStatistics

**Contents:**
- ExternalGPUStatistics
- Navigation
- Interfaces



---

## ExternalSource

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ExternalSource

**Contents:**
- ExternalSource
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Functions
  - Public

uint32 UE::DatasmithImporter::GetTypeHash ( const FSourceUri& SourceUri )



---

## Fab

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Fab

**Contents:**
- Fab
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## FacialAnimationEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/FacialAnimationEditor

**Contents:**
- FacialAnimationEditor
- Navigation
- Structs



---

## FacialAnimation

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/FacialAnimation

**Contents:**
- FacialAnimation
- Navigation
- Classes



---

## FastbuildController

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/FastbuildController

**Contents:**
- FastbuildController
- Navigation
- Classes
- Enums
  - Public



---

## FastGeoStreaming

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/FastGeoStreaming

**Contents:**
- FastGeoStreaming
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

uint32 EnumToIndex ( EFastGeoTransform Value )



---

## FbxAutomationTestBuilder

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/FbxAutomationTestBuilder

**Contents:**
- FbxAutomationTestBuilder
- Navigation
- Classes



---

## FieldNotificationTrace

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/FieldNotificationTrace

**Contents:**
- FieldNotificationTrace
- Navigation



---

## FieldSystemEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/FieldSystemEditor

**Contents:**
- FieldSystemEditor
- Navigation
- Classes
- Interfaces



---

## FileLogging

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/FileLogging

**Contents:**
- FileLogging
- Navigation
- Classes



---

## FloatingProperties

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/FloatingProperties

**Contents:**
- FloatingProperties
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## FractureEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/FractureEditor

**Contents:**
- FractureEditor
- Navigation
- Classes
- Structs
- Enums
  - Public
- Constants
- Variables
  - Public



---

## FractureEngine

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/FractureEngine

**Contents:**
- FractureEngine
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## FullBodyIK

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/FullBodyIK

**Contents:**
- FullBodyIK
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Functions
  - Public

void JacobianIK::AllocateMatrix ( Eigen::MatrixXf& InOutMatrix, const TArray< FFBIKLinkData >& InLinkData, int32 NumLinkComponent, const TMap< int32, FFBIKEffectorTarget >& InEndEffectors, int32 NumEffectorComponent )



---

## FunctionalTestingEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/FunctionalTestingEditor

**Contents:**
- FunctionalTestingEditor
- Navigation
- Classes
- Interfaces



---

## GameFeaturesEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GameFeaturesEditor

**Contents:**
- GameFeaturesEditor
- Navigation
- Structs



---

## GameFeatures

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GameFeatures

**Contents:**
- GameFeatures
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

bool GameFeatureVersePathMapper::operator! ( EBuildLookupOptions E )

EBuildLookupOptions GameFeatureVersePathMapper::operator& ( EBuildLookupOptions Lhs, EBuildLookupOptions Rhs )

EBuildLookupOptions & GameFeatureVersePathMapper::operator&= ( EBuildLookupOptions& Lhs, EBuildLookupOptions Rhs )

EBuildLookupOptions GameFeatureVersePathMapper::operator^ ( EBuildLookupOptions Lhs, EBuildLookupOptions Rhs )

EBuildLookupOptions & GameFeatureVersePathMapper::operator^= ( EBuildLookupOptions& Lhs, EBuildLookupOptions Rhs )

EBuildLookupOptions GameFeatureVersePathMapper::operator| ( EBuildLookupOptions Lhs, EBuildLookupOptions Rhs )

EBuildLookupOptions & GameFeatureVersePathMapper::operator|= ( EBuildLookupOptions& Lhs, EBuildLookupOptions Rhs )

EBuildLookupOptions GameFeatureVersePathMapper::operator~ ( EBuildLookupOptions E )

void LexFromString ( EGameFeatureTargetState& Value, const TCHAR* StringIn )

void LexFromString ( EGameFeatureURLOptions& ValueOut, const FStringView& StringIn )

const FString LexToString ( const EBuiltInAutoState BuiltInAutoState )

const FString LexToString ( const EGameFeatureTargetState GameFeatureTargetState )

const TCHAR * LexToString ( EGameFeatureURLOptions InOption )

bool operator! ( EGameFeatureURLOptions E )

EGameFeatureURLOptions operator& ( EGameFeatureURLOptions Lhs, EGameFeatureURLOptions Rhs )

EGameFeatureURLOptions & operator&= ( EGameFeatureURLOptions& Lhs, EGameFeatureURLOptions Rhs )

EGameFeatureURLOptions operator^ ( EGameFeatureURLOptions Lhs, EGameFeatureURLOptions Rhs )

EGameFeatureURLOptions & operator^= ( EGameFeatureURLOptions& Lhs, EGameFeatureURLOptions Rhs )

EGameFeatureURLOptions operator| ( EGameFeatureURLOptions Lhs, EGameFeatureURLOptions Rhs )

EGameFeatureURLOptions & operator|= ( EGameFeatureURLOptions& Lhs, EGameFeatureURLOptions Rhs )

EGameFeatureURLOptions operator~ ( EGameFeatureURLOptions E )



---

## GameInputBase

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GameInputBase

**Contents:**
- GameInputBase
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## GameplayAbilitiesEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GameplayAbilitiesEditor

**Contents:**
- GameplayAbilitiesEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## GameplayAbilities

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GameplayAbilities

**Contents:**
- GameplayAbilities
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

FString EGameplayCueEventToString ( int32 Type )

FString EGameplayModEffectToString ( int32 Type )

FString EGameplayModOpToString ( int32 Type )

FString EGameplayModToString ( int32 Type )

bool EvaluateChannel ( const FMovieSceneGameplayCueChannel* InChannel, FFrameTime InTime, FMovieSceneGameplayCueKey& OutValue )

const GEComponentClass * FindParentComponent ( const GEComponentClass& ChildComponent )

float GameplayEffectUtilities::ComputeStackedModifierMagnitude ( float BaseComputedMagnitude, int32 StackCount, EGameplayModOp::Type ModOp )

float GameplayEffectUtilities::GetModifierBiasByModifierOp ( EGameplayModOp::Type ModOp )

PRAGMA_DISABLE_DEPRECATION_WARNINGSuint32 GetTypeHash ( const FGCNotifyActorKey& Key )

void InitGameplayAbilityTargetDataHandleNetSerializerTypeCache()

void InitGameplayEffectContextHandleNetSerializerTypeCache()

bool operator! ( EConsiderPending E )

bool operator! ( EGameplayCueExecutionOptions E )

EConsiderPending operator& ( EConsiderPending Lhs, EConsiderPending Rhs )

EGameplayCueExecutionOptions operator& ( EGameplayCueExecutionOptions Lhs, EGameplayCueExecutionOptions Rhs )

EConsiderPending & operator&= ( EConsiderPending& Lhs, EConsiderPending Rhs )

EGameplayCueExecutionOptions & operator&= ( EGameplayCueExecutionOptions& Lhs, EGameplayCueExecutionOptions Rhs )

EConsiderPending operator^ ( EConsiderPending Lhs, EConsiderPending Rhs )

EGameplayCueExecutionOptions operator^ ( EGameplayCueExecutionOptions Lhs, EGameplayCueExecutionOptions Rhs )

EConsiderPending & operator^= ( EConsiderPending& Lhs, EConsiderPending Rhs )

EGameplayCueExecutionOptions & operator^= ( EGameplayCueExecutionOptions& Lhs, EGameplayCueExecutionOptions Rhs )

EConsiderPending operator| ( EConsiderPending Lhs, EConsiderPending Rhs )

EGameplayCueExecutionOptions operator| ( EGameplayCueExecutionOptions Lhs, EGameplayCueExecutionOptions Rhs )

EConsiderPending & operator|= ( EConsiderPending& Lhs, EConsiderPending Rhs )

EGameplayCueExecutionOptions & operator|= ( EGameplayCueExecutionOptions& Lhs, EGameplayCueExecutionOptions Rhs )

EConsiderPending operator~ ( EConsiderPending E )

EGameplayCueExecutionOptions operator~ ( EGameplayCueExecutionOptions E )

bool operator== ( const FGCNotifyActorKey& Other ) const



---

## GameplayBehaviorsEditorModule

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GameplayBehaviorsEditorModule

**Contents:**
- GameplayBehaviorsEditorModule
- Navigation
- Interfaces



---

## GameplayBehaviorSmartObjectsModule

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GameplayBehaviorSmartObjectsModu-

**Contents:**
- GameplayBehaviorSmartObjectsModule
- Navigation
- Classes
- Structs
- Interfaces



---

## GameplayBehaviorsModule

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GameplayBehaviorsModule

**Contents:**
- GameplayBehaviorsModule
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## GameplayCamerasEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GameplayCamerasEditor

**Contents:**
- GameplayCamerasEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## GameplayCameras

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GameplayCameras

**Contents:**
- GameplayCameras
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

bool CameraParameterValueEquals ( typename TCallTraits< ValueType >::ParamType A, typename TCallTraits< ValueType >::ParamType B )

bool operator! ( ECameraNodeFlags E )

bool operator! ( ECameraRigLayer E )

bool operator! ( EObjectTreeGraphObjectSupportFlags E )

ECameraNodeFlags operator& ( ECameraNodeFlags Lhs, ECameraNodeFlags Rhs )

ECameraRigLayer operator& ( ECameraRigLayer Lhs, ECameraRigLayer Rhs )

EObjectTreeGraphObjectSupportFlags operator& ( EObjectTreeGraphObjectSupportFlags Lhs, EObjectTreeGraphObjectSupportFlags Rhs )

ECameraNodeFlags & operator&= ( ECameraNodeFlags& Lhs, ECameraNodeFlags Rhs )

ECameraRigLayer & operator&= ( ECameraRigLayer& Lhs, ECameraRigLayer Rhs )

EObjectTreeGraphObjectSupportFlags & operator&= ( EObjectTreeGraphObjectSupportFlags& Lhs, EObjectTreeGraphObjectSupportFlags Rhs )

ECameraNodeFlags operator^ ( ECameraNodeFlags Lhs, ECameraNodeFlags Rhs )

ECameraRigLayer operator^ ( ECameraRigLayer Lhs, ECameraRigLayer Rhs )

EObjectTreeGraphObjectSupportFlags operator^ ( EObjectTreeGraphObjectSupportFlags Lhs, EObjectTreeGraphObjectSupportFlags Rhs )

ECameraNodeFlags & operator^= ( ECameraNodeFlags& Lhs, ECameraNodeFlags Rhs )

ECameraRigLayer & operator^= ( ECameraRigLayer& Lhs, ECameraRigLayer Rhs )

EObjectTreeGraphObjectSupportFlags & operator^= ( EObjectTreeGraphObjectSupportFlags& Lhs, EObjectTreeGraphObjectSupportFlags Rhs )

ECameraNodeFlags operator| ( ECameraNodeFlags Lhs, ECameraNodeFlags Rhs )

ECameraRigLayer operator| ( ECameraRigLayer Lhs, ECameraRigLayer Rhs )

EObjectTreeGraphObjectSupportFlags operator| ( EObjectTreeGraphObjectSupportFlags Lhs, EObjectTreeGraphObjectSupportFlags Rhs )

ECameraNodeFlags & operator|= ( ECameraNodeFlags& Lhs, ECameraNodeFlags Rhs )

ECameraRigLayer & operator|= ( ECameraRigLayer& Lhs, ECameraRigLayer Rhs )

EObjectTreeGraphObjectSupportFlags & operator|= ( EObjectTreeGraphObjectSupportFlags& Lhs, EObjectTreeGraphObjectSupportFlags Rhs )

ECameraNodeFlags operator~ ( ECameraNodeFlags E )

ECameraRigLayer operator~ ( ECameraRigLayer E )

EObjectTreeGraphObjectSupportFlags operator~ ( EObjectTreeGraphObjectSupportFlags E )

bool UE::Cameras::operator! ( ECameraContextDataTableFilter E )

bool UE::Cameras::operator! ( FCameraContextDataTable::EEntryFlags E )

bool UE::Cameras::operator! ( ECameraEvaluationServiceFlags E )

bool UE::Cameras::operator! ( ECameraNodeEvaluatorFlags E )

bool UE::Cameras::operator! ( ECameraVariableTableFilter E )

bool UE::Cameras::operator! ( FCameraVariableTable::EEntryFlags E )

bool UE::Cameras::operator! ( ECameraDebugBlockBuildVisitFlags E )

bool UE::Cameras::operator! ( ECameraDebugDrawVisitFlags E )

ECameraContextDataTableFilter UE::Cameras::operator& ( ECameraContextDataTableFilter Lhs, ECameraContextDataTableFilter Rhs )

FCameraContextDataTable::EEntryFlags UE::Cameras::operator& ( FCameraContextDataTable::EEntryFlags Lhs, FCameraContextDataTable::EEntryFlags Rhs )

ECameraEvaluationServiceFlags UE::Cameras::operator& ( ECameraEvaluationServiceFlags Lhs, ECameraEvaluationServiceFlags Rhs )

ECameraNodeEvaluatorFlags UE::Cameras::operator& ( ECameraNodeEvaluatorFlags Lhs, ECameraNodeEvaluatorFlags Rhs )

ECameraVariableTableFilter UE::Cameras::operator& ( ECameraVariableTableFilter Lhs, ECameraVariableTableFilter Rhs )

FCameraVariableTable::EEntryFlags UE::Cameras::operator& ( FCameraVariableTable::EEntryFlags Lhs, FCameraVariableTable::EEntryFlags Rhs )

ECameraDebugBlockBuildVisitFlags UE::Cameras::operator& ( ECameraDebugBlockBuildVisitFlags Lhs, ECameraDebugBlockBuildVisitFlags Rhs )

ECameraDebugDrawVisitFlags UE::Cameras::operator& ( ECameraDebugDrawVisitFlags Lhs, ECameraDebugDrawVisitFlags Rhs )

ECameraContextDataTableFilter & UE::Cameras::operator&= ( ECameraContextDataTableFilter& Lhs, ECameraContextDataTableFilter Rhs )

FCameraContextDataTable::EEntryFlags & UE::Cameras::operator&= ( FCameraContextDataTable::EEntryFlags& Lhs, FCameraContextDataTable::EEntryFlags Rhs )

ECameraEvaluationServiceFlags & UE::Cameras::operator&= ( ECameraEvaluationServiceFlags& Lhs, ECameraEvaluationServiceFlags Rhs )

ECameraNodeEvaluatorFlags & UE::Cameras::operator&= ( ECameraNodeEvaluatorFlags& Lhs, ECameraNodeEvaluatorFlags Rhs )

ECameraVariableTableFilter & UE::Cameras::operator&= ( ECameraVariableTableFilter& Lhs, ECameraVariableTableFilter Rhs )

FCameraVariableTable::EEntryFlags & UE::Cameras::operator&= ( FCameraVariableTable::EEntryFlags& Lhs, FCameraVariableTable::EEntryFlags Rhs )

ECameraDebugBlockBuildVisitFlags & UE::Cameras::operator&= ( ECameraDebugBlockBuildVisitFlags& Lhs, ECameraDebugBlockBuildVisitFlags Rhs )

ECameraDebugDrawVisitFlags & UE::Cameras::operator&= ( ECameraDebugDrawVisitFlags& Lhs, ECameraDebugDrawVisitFlags Rhs )

ECameraContextDataTableFilter UE::Cameras::operator^ ( ECameraContextDataTableFilter Lhs, ECameraContextDataTableFilter Rhs )

FCameraContextDataTable::EEntryFlags UE::Cameras::operator^ ( FCameraContextDataTable::EEntryFlags Lhs, FCameraContextDataTable::EEntryFlags Rhs )

ECameraEvaluationServiceFlags UE::Cameras::operator^ ( ECameraEvaluationServiceFlags Lhs, ECameraEvaluationServiceFlags Rhs )

ECameraNodeEvaluatorFlags UE::Cameras::operator^ ( ECameraNodeEvaluatorFlags Lhs, ECameraNodeEvaluatorFlags Rhs )

ECameraVariableTableFilter UE::Cameras::operator^ ( ECameraVariableTableFilter Lhs, ECameraVariableTableFilter Rhs )

FCameraVariableTable::EEntryFlags UE::Cameras::operator^ ( FCameraVariableTable::EEntryFlags Lhs, FCameraVariableTable::EEntryFlags Rhs )

ECameraDebugBlockBuildVisitFlags UE::Cameras::operator^ ( ECameraDebugBlockBuildVisitFlags Lhs, ECameraDebugBlockBuildVisitFlags Rhs )

ECameraDebugDrawVisitFlags UE::Cameras::operator^ ( ECameraDebugDrawVisitFlags Lhs, ECameraDebugDrawVisitFlags Rhs )

ECameraContextDataTableFilter & UE::Cameras::operator^= ( ECameraContextDataTableFilter& Lhs, ECameraContextDataTableFilter Rhs )

FCameraContextDataTable::EEntryFlags & UE::Cameras::operator^= ( FCameraContextDataTable::EEntryFlags& Lhs, FCameraContextDataTable::EEntryFlags Rhs )

ECameraEvaluationServiceFlags & UE::Cameras::operator^= ( ECameraEvaluationServiceFlags& Lhs, ECameraEvaluationServiceFlags Rhs )

ECameraNodeEvaluatorFlags & UE::Cameras::operator^= ( ECameraNodeEvaluatorFlags& Lhs, ECameraNodeEvaluatorFlags Rhs )

ECameraVariableTableFilter & UE::Cameras::operator^= ( ECameraVariableTableFilter& Lhs, ECameraVariableTableFilter Rhs )

FCameraVariableTable::EEntryFlags & UE::Cameras::operator^= ( FCameraVariableTable::EEntryFlags& Lhs, FCameraVariableTable::EEntryFlags Rhs )

ECameraDebugBlockBuildVisitFlags & UE::Cameras::operator^= ( ECameraDebugBlockBuildVisitFlags& Lhs, ECameraDebugBlockBuildVisitFlags Rhs )

ECameraDebugDrawVisitFlags & UE::Cameras::operator^= ( ECameraDebugDrawVisitFlags& Lhs, ECameraDebugDrawVisitFlags Rhs )

ECameraContextDataTableFilter UE::Cameras::operator| ( ECameraContextDataTableFilter Lhs, ECameraContextDataTableFilter Rhs )

FCameraContextDataTable::EEntryFlags UE::Cameras::operator| ( FCameraContextDataTable::EEntryFlags Lhs, FCameraContextDataTable::EEntryFlags Rhs )

ECameraEvaluationServiceFlags UE::Cameras::operator| ( ECameraEvaluationServiceFlags Lhs, ECameraEvaluationServiceFlags Rhs )

ECameraNodeEvaluatorFlags UE::Cameras::operator| ( ECameraNodeEvaluatorFlags Lhs, ECameraNodeEvaluatorFlags Rhs )

ECameraVariableTableFilter UE::Cameras::operator| ( ECameraVariableTableFilter Lhs, ECameraVariableTableFilter Rhs )

FCameraVariableTable::EEntryFlags UE::Cameras::operator| ( FCameraVariableTable::EEntryFlags Lhs, FCameraVariableTable::EEntryFlags Rhs )

ECameraDebugBlockBuildVisitFlags UE::Cameras::operator| ( ECameraDebugBlockBuildVisitFlags Lhs, ECameraDebugBlockBuildVisitFlags Rhs )

ECameraDebugDrawVisitFlags UE::Cameras::operator| ( ECameraDebugDrawVisitFlags Lhs, ECameraDebugDrawVisitFlags Rhs )

ECameraContextDataTableFilter & UE::Cameras::operator|= ( ECameraContextDataTableFilter& Lhs, ECameraContextDataTableFilter Rhs )

FCameraContextDataTable::EEntryFlags & UE::Cameras::operator|= ( FCameraContextDataTable::EEntryFlags& Lhs, FCameraContextDataTable::EEntryFlags Rhs )

ECameraEvaluationServiceFlags & UE::Cameras::operator|= ( ECameraEvaluationServiceFlags& Lhs, ECameraEvaluationServiceFlags Rhs )

ECameraNodeEvaluatorFlags & UE::Cameras::operator|= ( ECameraNodeEvaluatorFlags& Lhs, ECameraNodeEvaluatorFlags Rhs )

ECameraVariableTableFilter & UE::Cameras::operator|= ( ECameraVariableTableFilter& Lhs, ECameraVariableTableFilter Rhs )

FCameraVariableTable::EEntryFlags & UE::Cameras::operator|= ( FCameraVariableTable::EEntryFlags& Lhs, FCameraVariableTable::EEntryFlags Rhs )

ECameraDebugBlockBuildVisitFlags & UE::Cameras::operator|= ( ECameraDebugBlockBuildVisitFlags& Lhs, ECameraDebugBlockBuildVisitFlags Rhs )

ECameraDebugDrawVisitFlags & UE::Cameras::operator|= ( ECameraDebugDrawVisitFlags& Lhs, ECameraDebugDrawVisitFlags Rhs )

ECameraContextDataTableFilter UE::Cameras::operator~ ( ECameraContextDataTableFilter E )

FCameraContextDataTable::EEntryFlags UE::Cameras::operator~ ( FCameraContextDataTable::EEntryFlags E )

ECameraEvaluationServiceFlags UE::Cameras::operator~ ( ECameraEvaluationServiceFlags E )

ECameraNodeEvaluatorFlags UE::Cameras::operator~ ( ECameraNodeEvaluatorFlags E )

ECameraVariableTableFilter UE::Cameras::operator~ ( ECameraVariableTableFilter E )

FCameraVariableTable::EEntryFlags UE::Cameras::operator~ ( FCameraVariableTable::EEntryFlags E )

ECameraDebugBlockBuildVisitFlags UE::Cameras::operator~ ( ECameraDebugBlockBuildVisitFlags E )

ECameraDebugDrawVisitFlags UE::Cameras::operator~ ( ECameraDebugDrawVisitFlags E )

float UE::Cameras::SmootherStep ( float Value )

float UE::Cameras::SmoothStep ( float Value )

FString UE::Cameras::ToDebugString ( const FieldType& FieldValue )

FString UE::Cameras::ToDebugString ( TEnumAsByte< EnumType > EnumValue )

FString UE::Cameras::ToDebugString ( const UE::Math::TVector< T >& FieldValue )

FString UE::Cameras::ToDebugString ( const UE::Math::TVector2< T >& FieldValue )

FString UE::Cameras::ToDebugString ( const UE::Math::TVector4< T >& FieldValue )

FString UE::Cameras::ToDebugString ( const UE::Math::TRotator< T >& FieldValue )

FString UE::Cameras::ToDebugString ( const UE::Math::TTransform< T >& FieldValue )

FString UE::Cameras::ToDebugString ( const FLinearColor& FieldValue )

FString UE::Cameras::ToDebugString ( const EAspectRatioAxisConstraint& FieldValue )

FString UE::Cameras::ToDebugString ( const ECameraProjectionMode::Type& FieldValue )



---

## GameplayGraph

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GameplayGraph

**Contents:**
- GameplayGraph
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

bool operator! ( EGraphIslandOperations E )

EGraphIslandOperations operator& ( EGraphIslandOperations Lhs, EGraphIslandOperations Rhs )

EGraphIslandOperations & operator&= ( EGraphIslandOperations& Lhs, EGraphIslandOperations Rhs )

EGraphIslandOperations operator^ ( EGraphIslandOperations Lhs, EGraphIslandOperations Rhs )

EGraphIslandOperations & operator^= ( EGraphIslandOperations& Lhs, EGraphIslandOperations Rhs )

EGraphIslandOperations operator| ( EGraphIslandOperations Lhs, EGraphIslandOperations Rhs )

EGraphIslandOperations & operator|= ( EGraphIslandOperations& Lhs, EGraphIslandOperations Rhs )

EGraphIslandOperations operator~ ( EGraphIslandOperations E )



---

## GameplayInsightsEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GameplayInsightsEditor

**Contents:**
- GameplayInsightsEditor
- Navigation
- Classes



---

## GameplayInsights

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GameplayInsights

**Contents:**
- GameplayInsights
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## GameplayInteractionsModule

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GameplayInteractionsModule

**Contents:**
- GameplayInteractionsModule
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Variables
  - Public



---

## GameplayStateTreeModule

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GameplayStateTreeModule

**Contents:**
- GameplayStateTreeModule
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## GameplayTagsEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GameplayTagsEditor

**Contents:**
- GameplayTagsEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## Gauntlet

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Gauntlet

**Contents:**
- Gauntlet
- Navigation
- Classes
- Structs



---

## GeForceNOWWrapper

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeForceNOWWrapper

**Contents:**
- GeForceNOWWrapper
- Navigation
- Interfaces



---

## GeneSplicerLibTest

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeneSplicerLibTest

**Contents:**
- GeneSplicerLibTest
- Navigation
- Classes



---

## GeneSplicerLib

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeneSplicerLib

**Contents:**
- GeneSplicerLib
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public



---

## GeneSplicerModule

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeneSplicerModule

**Contents:**
- GeneSplicerModule
- Navigation
- Classes
- Enums
  - Public
- Functions
  - Public

bool operator! ( EGenePoolMask E )

EGenePoolMask operator& ( EGenePoolMask Lhs, EGenePoolMask Rhs )

EGenePoolMask & operator&= ( EGenePoolMask& Lhs, EGenePoolMask Rhs )

EGenePoolMask operator^ ( EGenePoolMask Lhs, EGenePoolMask Rhs )

EGenePoolMask & operator^= ( EGenePoolMask& Lhs, EGenePoolMask Rhs )

EGenePoolMask operator| ( EGenePoolMask Lhs, EGenePoolMask Rhs )

EGenePoolMask & operator|= ( EGenePoolMask& Lhs, EGenePoolMask Rhs )

EGenePoolMask operator~ ( EGenePoolMask E )



---

## GeometryAlgorithms

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryAlgorithms

**Contents:**
- GeometryAlgorithms
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public



---

## GeometryCacheAbcFile

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryCacheAbcFile

**Contents:**
- GeometryCacheAbcFile
- Navigation
- Classes



---

## GeometryCacheEd

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryCacheEd

**Contents:**
- GeometryCacheEd
- Navigation
- Classes



---

## GeometryCacheLevelSequenceBaker

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryCacheLevelSequenceBaker

**Contents:**
- GeometryCacheLevelSequenceBaker
- Navigation
- Classes



---

## GeometryCacheSequencer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryCacheSequencer

**Contents:**
- GeometryCacheSequencer
- Navigation
- Classes
- Variables
  - Public
- Functions
  - Static

static UGeometryCacheComponent * AcquireGeometryCacheFromObjectGuid ( const FGuid& Guid, TSharedPtr< ISequencer > SequencerPtr )



---

## GeometryCacheStreamer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryCacheStreamer

**Contents:**
- GeometryCacheStreamer
- Navigation
- Classes
- Structs
- Interfaces



---

## GeometryCacheTracks

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryCacheTracks

**Contents:**
- GeometryCacheTracks
- Navigation
- Classes
- Structs



---

## GeometryCacheUSD

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryCacheUSD

**Contents:**
- GeometryCacheUSD
- Navigation
- Classes
- Typedefs



---

## GeometryCache

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryCache

**Contents:**
- GeometryCache
- Navigation
- Classes
- Structs
- Interfaces
- Constants
- Variables
  - Public



---

## GeometryCollectionDepNodes

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryCollectionDepNodes

**Contents:**
- GeometryCollectionDepNodes
- Navigation
- Interfaces



---

## GeometryCollectionEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryCollectionEditor

**Contents:**
- GeometryCollectionEditor
- Navigation
- Classes
- Interfaces
- Typedefs



---

## GeometryCollectionNodes

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryCollectionNodes

**Contents:**
- GeometryCollectionNodes
- Navigation
- Structs
- Interfaces
- Enums
  - Public
- Variables
  - Public
- Functions
  - Public

virtual void Evaluate ( UE::Dataflow::FContext& Context, const FDataflowOutput* Out ) const

FSkeletonToCollectionDataflowNode ( const UE::Dataflow::FNodeParameters& InParam, FGuid InGuid )



---

## GeometryCollectionSequencer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryCollectionSequencer

**Contents:**
- GeometryCollectionSequencer
- Navigation
- Classes



---

## GeometryCollectionTracks

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryCollectionTracks

**Contents:**
- GeometryCollectionTracks
- Navigation
- Classes
- Structs



---

## GeometryDataflowNodes

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryDataflowNodes

**Contents:**
- GeometryDataflowNodes
- Navigation
- Structs
- Interfaces
- Enums
  - Public



---

## GeometryFlowCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryFlowCore

**Contents:**
- GeometryFlowCore
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

NodeType * UE::GeometryFlow::CastToNodePtr ( FNode* Node )

EGeometryFlowResult UE::GeometryFlow::ExtractData ( TSafeSharedPtr< IData > Data, T& Storage, int32 StorageTypeIdentifier, bool bTryTakeResult )

TArray< int > UE::GeometryFlow::FindAllConnectionsToNode ( FGraph::FHandle ToNodeID, const TArray< FGraph::FConnection >& Connections )

int UE::GeometryFlow::FindAnyConnectionFromNode ( FGraph::FHandle FromNode, const TArray< FGraph::FConnection >& Connections )

int UE::GeometryFlow::FindAnyConnectionToNode ( FGraph::FHandle ToNode, const TArray< FGraph::FConnection >& Connections )

uint32 UE::GeometryFlow::GetTypeHash ( FGraph::FHandle Handle )

TUniquePtr< TBasicNodeInput< DataType, DataType::DataTypeIdentifier > > UE::GeometryFlow::MakeBasicInput()

TUniquePtr< TBasicNodeOutput< DataType, DataType::DataTypeIdentifier > > UE::GeometryFlow::MakeBasicOutput()

TSafeSharedPtr< TMovableData< DataType, DataType::DataTypeIdentifier > > UE::GeometryFlow::MakeMovableData ( DataType&& Data )

TSafeSharedPtr< T > UE::GeometryFlow::MakeSafeShared ( InArgTypes&&... Args )

void UE::GeometryFlow::UpdateSettingsSourceNodeValue ( FGraph& Graph, FGraph::FHandle NodeHandle, const SettingsType& NewSettings )

void UE::GeometryFlow::UpdateSourceNodeValue ( FGraph& Graph, FGraph::FHandle NodeHandle, const typename SourceNodeType::CppType& NewValue )

void UE::GeometryFlow::UpdateSwitchNodeInputIndex ( FGraph& Graph, FGraph::FHandle NodeHandle, int32 NewSwitchIndex )



---

## GeometryFlowMeshProcessingEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryFlowMeshProcessingEditor

**Contents:**
- GeometryFlowMeshProcessingEditor
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## GeometryFlowMeshProcessing

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryFlowMeshProcessing

**Contents:**
- GeometryFlowMeshProcessing
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

void UE::GeometryFlow::Private::LogMeshProcessing ( const TCHAR* Identifier, const TCHAR* Message )



---

## GeometryMaskEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryMaskEditor

**Contents:**
- GeometryMaskEditor
- Navigation
- Classes



---

## GeometryMask

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryMask

**Contents:**
- GeometryMask
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Functions

bool operator! ( EGeometryMaskColorChannel E )

EGeometryMaskColorChannel operator& ( EGeometryMaskColorChannel Lhs, EGeometryMaskColorChannel Rhs )

EGeometryMaskColorChannel & operator&= ( EGeometryMaskColorChannel& Lhs, EGeometryMaskColorChannel Rhs )

EGeometryMaskColorChannel operator^ ( EGeometryMaskColorChannel Lhs, EGeometryMaskColorChannel Rhs )

EGeometryMaskColorChannel & operator^= ( EGeometryMaskColorChannel& Lhs, EGeometryMaskColorChannel Rhs )

EGeometryMaskColorChannel operator| ( EGeometryMaskColorChannel Lhs, EGeometryMaskColorChannel Rhs )

EGeometryMaskColorChannel & operator|= ( EGeometryMaskColorChannel& Lhs, EGeometryMaskColorChannel Rhs )

EGeometryMaskColorChannel operator~ ( EGeometryMaskColorChannel E )



---

## GeometryMode

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryMode

**Contents:**
- GeometryMode
- Navigation
- Classes
- Structs
- Typedefs



---

## GeometryProcessingAdapters

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryProcessingAdapters

**Contents:**
- GeometryProcessingAdapters
- Navigation
- Classes



---

## GeometryScriptingCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryScriptingCore

**Contents:**
- GeometryScriptingCore
- Navigation
- Classes
- Structs
- Enums
  - Public
- Variables
  - Public



---

## GeometryScriptingEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeometryScriptingEditor

**Contents:**
- GeometryScriptingEditor
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## GeoReferencingEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeoReferencingEditor

**Contents:**
- GeoReferencingEditor
- Navigation
- Classes



---

## GeoReferencing

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GeoReferencing

**Contents:**
- GeoReferencing
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## GizmoEdMode

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GizmoEdMode

**Contents:**
- GizmoEdMode
- Navigation
- Classes
- Interfaces
- Enums
  - Public



---

## GizmoSettings

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GizmoSettings

**Contents:**
- GizmoSettings
- Navigation



---

## GlobalConfigurationDataCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GlobalConfigurationDataCore

**Contents:**
- GlobalConfigurationDataCore
- Navigation
- Classes
- Interfaces
- Functions
  - Public

Type UE::GlobalConfigurationData::GetDataWithDefault ( const FString& EntryName, const Type& DefaultValue )

bool UE::GlobalConfigurationData::TryGetData ( const FString& EntryName, bool& bValueOut )

bool UE::GlobalConfigurationData::TryGetData ( const FString& EntryName, int32& ValueOut )

bool UE::GlobalConfigurationData::TryGetData ( const FString& EntryName, float& ValueOut )

bool UE::GlobalConfigurationData::TryGetData ( const FString& EntryName, FString& ValueOut )

bool UE::GlobalConfigurationData::TryGetData ( const FString& EntryName, FText& ValueOut )

bool UE::GlobalConfigurationData::TryGetData ( const FString& EntryName, Type& DataOut )

bool UE::GlobalConfigurationData::TryGetData ( const FString& EntryName, Type* DataOut )

bool UE::GlobalConfigurationData::TryGetDataOfType ( const FString& EntryName, const UStruct* Type, void* DataOut )



---

## GlobalConfigurationData

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GlobalConfigurationData

**Contents:**
- GlobalConfigurationData
- Navigation
- Classes



---

## GLTFCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GLTFCore

**Contents:**
- GLTFCore
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## GLTFExporter

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GLTFExporter

**Contents:**
- GLTFExporter
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## GoogleARCoreBase

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GoogleARCoreBase

**Contents:**
- GoogleARCoreBase
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

ENUM_CLASS_FLAGS ( EGoogleARCoreLineTraceChannel )



---

## GoogleARCoreRendering

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GoogleARCoreRendering

**Contents:**
- GoogleARCoreRendering
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## GoogleARCoreServices

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GoogleARCoreServices

**Contents:**
- GoogleARCoreServices
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Functions
  - Public

DEFINE_LOG_CATEGORY_STATIC ( LogGoogleARCoreServices, Log, All )



---

## GooglePADEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GooglePADEditor

**Contents:**
- GooglePADEditor
- Navigation
- Classes



---

## GooglePAD

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GooglePAD

**Contents:**
- GooglePAD
- Navigation
- Classes
- Enums
  - Public



---

## GPULightmass

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GPULightmass

**Contents:**
- GPULightmass
- Navigation
- Classes
- Enums
  - Public



---

## GPUTextureTransfer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GPUTextureTransfer

**Contents:**
- GPUTextureTransfer
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## HairCardGeneratorDataflow

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HairCardGeneratorDataflow

**Contents:**
- HairCardGeneratorDataflow
- Navigation
- Classes
- Structs



---

## HairCardGeneratorEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HairCardGeneratorEditor

**Contents:**
- HairCardGeneratorEditor
- Navigation
- Classes
- Structs
- Interfaces



---

## HairCardGeneratorFramework

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HairCardGeneratorFramework

**Contents:**
- HairCardGeneratorFramework
- Navigation
- Interfaces
- Functions
  - Public

void HairCardGenerator_Utils::RegisterModularHairCardGenerator ( IHairCardGenerator* Generator )

void HairCardGenerator_Utils::UnregisterModularHairCardGenerator ( IHairCardGenerator* Generator )



---

## HairModelingToolset

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HairModelingToolset

**Contents:**
- HairModelingToolset
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## HairStrandsCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HairStrandsCore

**Contents:**
- HairStrandsCore
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

void AddClearAABBPass ( FRDGBuilder& GraphBuilder, FGlobalShaderMap* ShaderMap, uint32 AABBCount, FRDGBufferUAVRef& OutAABBUAV )

void AddComputeMipsPass ( FRDGBuilder& GraphBuilder, FGlobalShaderMap* ShaderMap, FRDGTextureRef& OutTexture )

void AddDeformSimHairStrandsPass ( FRDGBuilder& GraphBuilder, FGlobalShaderMap* ShaderMap, const uint32 InstanceRegisteredIndex, const uint32 MeshLODIndex, const uint32 VertexCount, FHairStrandsRestRootResource* SimRestRootResources, FHairStrandsDeformedRootResource* SimDeformedRootResources, FRDGBufferSRVRef SimRestPosePositionBuffer, FRDGBufferSRVRef SimPointToCurveBuffer, FRDGImportedBuffer& OutSimDeformedPositionBuffer, const FVector& SimRestOffset, FRDGBufferSRVRef SimDeformedOffsetBuffer, const bool bHasGlobalInterpolation, FRHIShaderResourceView* BoneBufferSRV )

void AddGroomCacheUpdatePass ( FRDGBuilder& GraphBuilder, FGlobalShaderMap* ShaderMap, uint32 InstanceRegisteredIndex, uint32 PointCount, uint32 CurveCount, float InterpolationFactor, float InMaxHairRadius, bool bAllowAddedControlPoint, FGroomCacheResources CacheResources0, FGroomCacheResources CacheResources1, FRDGBufferSRVRef InRestPositionBuffer, FRDGBufferSRVRef InRestCurveBuffer, FRDGBufferSRVRef InRestPointToCurveBuffer, FRDGBufferSRVRef InDeformedOffsetBuffer, FRDGBufferUAVRef OutBuffer )

void AddHairCardsDeformationPass ( FRDGBuilder& GraphBuilder, FGlobalShaderMap* ShaderMap, const ERHIFeatureLevel::Type FeatureLevel, const FShaderPrintData* ShaderPrintData, FHairGroupInstance* Instance, const int32 HairLODIndex, const int32 MeshLODIndex, ERHIPipeline CardPositionExternalAccessPipeline )

void AddHairCardsRBFInterpolationPass ( FRDGBuilder& GraphBuilder, FGlobalShaderMap* ShaderMap, const int32 MeshLODIndex, FHairCardsRestResource* RestResources, FHairCardsDeformedResource* DeformedResources, FHairStrandsRestRootResource* RestRootResources, FHairStrandsDeformedRootResource* DeformedRootResources )

void AddHairMeshesRBFInterpolationPass ( FRDGBuilder& GraphBuilder, FGlobalShaderMap* ShaderMap, const int32 MeshLODIndex, FHairMeshesRestResource* RestResources, FHairMeshesDeformedResource* DeformedResources, FHairStrandsRestRootResource* RestRootResources, FHairStrandsDeformedRootResource* DeformedRootResources )

void AddHairStrandInitMeshSamplesPass ( FRDGBuilder& GraphBuilder, FGlobalShaderMap* ShaderMap, const int32 MeshLODIndex, const FCachedGeometry& MeshLODData, FHairStrandsRestRootResource* RestResources, FHairStrandsDeformedRootResource* DeformedResources )

void AddHairStrandsInterpolationPass ( FRDGBuilder& GraphBuilder, FGlobalShaderMap* ShaderMap, EShaderPlatform InPlatform, const FShaderPrintData* ShaderPrintData, const FHairGroupInstance* Instance, const uint32 VertexCount, const uint32 CurveCount, const uint32 MaxPointPerCurve, const int32 MeshLODIndex, const float HairLengthScale, const EHairInterpolationType HairInterpolationType, const EHairGeometryType InstanceGeometryType, const FRDGHairStrandsCullingData& CullingData, const FVector& InRenHairWorldOffset, const FVector& InSimHairWorldOffset, const FRDGBufferSRVRef& OutRenHairPositionOffsetBuffer, const FRDGBufferSRVRef& OutSimHairPositionOffsetBuffer, const FHairStrandsRestRootResource* RenRestRootResources, const FHairStrandsRestRootResource* SimRestRootResources, const FHairStrandsDeformedRootResource* RenDeformedRootResources, const FHairStrandsDeformedRootResource* SimDeformedRootResources, const FRDGBufferSRVRef& RenRestPosePositionBuffer, const FRDGBufferSRVRef& RenCurveBuffer, const bool bUseSingleGuide, const FRDGBufferSRVRef& CurveInterpolationBuffer, const FRDGBufferSRVRef& PoinInterpolationBuffer, const FRDGBufferSRVRef& SimRestPosePositionBuffer, const FRDGBufferSRVRef& SimDeformedPositionBuffer, const FRDGBufferSRVRef& RenDeformerPositionBuffer, FRDGBufferUAVRef& OutRenPositionBuffer, const FHairStrandsLODDeformedRootResource::EFrameType DeformedFrame )

void AddHairStrandUpdateMeshSamplesPass ( FRDGBuilder& GraphBuilder, FGlobalShaderMap* ShaderMap, const int32 MeshLODIndex, const FCachedGeometry& MeshLODData, FHairStrandsRestRootResource* RestResources, FHairStrandsDeformedRootResource* DeformedResources )

void AddHairStrandUpdateMeshTrianglesPass ( FRDGBuilder& GraphBuilder, FGlobalShaderMap* ShaderMap, const int32 MeshLODIndex, const FCachedGeometry& MeshLODData, FHairStrandsRestRootResource* RestResources, FHairStrandsDeformedRootResource* DeformedResources )

void AddHairStrandUpdatePositionOffsetPass ( FRDGBuilder& GraphBuilder, FGlobalShaderMap* ShaderMap, EHairPositionUpdateType UpdateType, const int32 InstanceRegisteredIndex, const int32 HairLODIndex, const int32 MeshLODIndex, FHairStrandsDeformedRootResource* DeformedRootResources, FHairStrandsDeformedResource* DeformedResources )

void AddHairTangentPass ( FRDGBuilder& GraphBuilder, FGlobalShaderMap* ShaderMap, uint32 PointCount, FHairGroupPublicData* HairGroupPublicData, FRDGBufferSRVRef PositionBuffer, FRDGBufferUAVRef OutTangentBuffer )

void AddPatchAttributePass ( FRDGBuilder& GraphBuilder, FGlobalShaderMap* ShaderMap, const uint32 CurveCount, const EHairPatchAttribute Mode, const bool bSimulation, const bool bUseSingleGuide, const FHairStrandsBulkData& RenBulkData, const FRDGBufferRef& RenAttributeBuffer, const FRDGBufferSRVRef& RenCurveBuffer, const FRDGBufferSRVRef& RenCurveToClusterIdBuffer, const FRDGBufferSRVRef& CurveInterpolationBuffer, const FRDGBufferSRVRef& PointInterpolationBuffer, FRDGImportedBuffer& OutRenAttributeBuffer )

void AddSkinUpdatePass ( FRDGBuilder& GraphBuilder, FGlobalShaderMap* ShaderMap, FSkeletalMeshLODRenderData& RenderData, const TArray< FSkinUpdateSection >& Sections, FRDGBufferRef OutDeformedPositionBuffer, FRDGBufferRef OutPrevDeformedPositionBuffer, FRDGBufferRef OutTangentBuffer )

void AddTransferPositionPass ( FRDGBuilder& GraphBuilder, FGlobalShaderMap* ShaderMap, const uint32 PointOffset, const uint32 PointCount, const uint32 TotalPointCount, FRDGBufferSRVRef InBuffer, FRDGBufferUAVRef OutBuffer )

void ComputeHairStrandsInterpolation ( FRDGBuilder& GraphBuilder, FGlobalShaderMap* ShaderMap, const uint32 ViewUniqueID, const uint32 ViewRayTracingMask, const EGroomViewMode ViewMode, const FVector& TranslatedWorldOffset, const FShaderPrintData* ShaderPrintData, FHairGroupInstance* Instance, int32 LODIndex, FHairStrandClusterData* ClusterData )

FHairGroupPublicData::FVertexFactoryInput ComputeHairStrandsVertexInputData ( const FHairGroupInstance* Instance, EGroomViewMode ViewMode )

void ComputeInterpolationWeights ( UGroomBindingAsset* BindingAsset, FSkeletalMeshRenderData* TargetRenderData, TArray< FRWBuffer >& TransferedPositions )

void ConvertFromGroomAsset ( UGroomAsset* In, FEditableGroom* Out, const bool bAllowCurveReordering, const bool bApplyDecimation, const bool bAllowAddEndControlPoint )

void ConvertToGroomAsset ( UGroomAsset* Out, const FEditableGroom* In, uint32 Operations )

FGroomCacheResources CreateGroomCacheBuffer ( FRDGBuilder& GraphBuilder, FGroomCacheVertexData& InVertexData )

UGroomImportOptions * CreateGroomImportOptions ( const FHairDescriptionGroups& GroupsDescription, const TArray< FHairGroupsInterpolation >& BuildSettings )

void CreateHairStrandsDebugDatas ( const FHairStrandsDatas& InData, FHairStrandsDebugDatas& Out )

void CreateHairStrandsDebugResources ( FRDGBuilder& GraphBuilder, const FHairStrandsDebugDatas* In, FHairStrandsDebugResources* Out )

void GenerateFolliculeMask ( FRDGBuilder& GraphBuilder, FGlobalShaderMap* ShaderMap, const EPixelFormat Format, const FIntPoint Resolution, const uint32 MipCount, const uint32 KernelSizeInPixels, const uint32 Channel, const TArray< FRDGBufferRef >& RootUVBuffers, FRDGTextureRef& OutTexture )

void GenerateFolliculeMask ( FRDGBuilder& GraphBuilder, FGlobalShaderMap* ShaderMap, const EPixelFormat Format, const FIntPoint Resolution, const uint32 MipCount, const uint32 KernelSizeInPixels, const uint32 Channel, const int32 LODIndex, FHairStrandsRestRootResource* RestResources, FRDGTextureRef& OutTexture )

uint32 GetBufferTotalNumBytes ( const FRDGExternalBuffer& In )

uint32 GetDataSize ( const FHairStrandsBulkData& BulkData )

uint32 GetDataSize ( const FHairStrandsInterpolationBulkData& InterpolationBulkData )

const FShaderParametersMetadata * GetForwardDeclaredShaderParametersStructMetadata ( const FHairCardsVertexFactoryUniformShaderParameters* DummyPtr )

const FShaderParametersMetadata * GetForwardDeclaredShaderParametersStructMetadata ( const FHairStrandsVertexFactoryUniformShaderParameters* DummyPtr )

const FLinearColor GetHairGroupDebugColor ( int32 GroupIt )

FHairGroupInstance * GetHairGroupInstance ( UGroomComponent* In, int32 InGroupIndex )

EHairResourceLoadingType GetHairResourceLoadingType ( EHairGeometryType InGeometryType, int32 InLODIndex )

float GetHairStrandsMaxLength ( const FHairStrandsDatas& In )

float GetHairStrandsMaxRadius ( const FHairStrandsDatas& In )

uint32 GetHairStrandsMaxSectionCount()

uint32 GetHairStrandsMaxTriangleCount()

uint32 GetHairTextureLayoutTextureCount ( EHairTextureLayout In )

const TCHAR * GetHairTextureLayoutTextureName ( EHairTextureLayout InLayout, uint32 InIndex, bool bDetail )

bool HasHairAttribute ( uint32 In, EHairAttribute InAttribute )

bool HasHairAttributeFlags ( uint32 In, EHairAttributeFlags InFlag )

FRDGHairStrandsCullingData ImportCullingData ( FRDGBuilder& GraphBuilder, FHairGroupPublicData* In )

bool operator! ( EGroomBindingAsyncProperties E )

bool operator! ( EGroomBindingAsyncPropertyLockType E )

bool operator! ( EGroomCacheAttributes E )

bool operator! ( EGroomCacheImportType E )

bool operator! ( EHairViewRayTracingMask E )

bool operator! ( EHairResourceStatus A )

EGroomBindingAsyncProperties operator& ( EGroomBindingAsyncProperties Lhs, EGroomBindingAsyncProperties Rhs )

EGroomBindingAsyncPropertyLockType operator& ( EGroomBindingAsyncPropertyLockType Lhs, EGroomBindingAsyncPropertyLockType Rhs )

EGroomCacheAttributes operator& ( EGroomCacheAttributes Lhs, EGroomCacheAttributes Rhs )

EGroomCacheImportType operator& ( EGroomCacheImportType Lhs, EGroomCacheImportType Rhs )

EHairViewRayTracingMask operator& ( EHairViewRayTracingMask Lhs, EHairViewRayTracingMask Rhs )

EHairResourceStatus operator& ( EHairResourceStatus In, EHairResourceStatus::EStatus InStatus )

EGroomBindingAsyncProperties & operator&= ( EGroomBindingAsyncProperties& Lhs, EGroomBindingAsyncProperties Rhs )

EGroomBindingAsyncPropertyLockType & operator&= ( EGroomBindingAsyncPropertyLockType& Lhs, EGroomBindingAsyncPropertyLockType Rhs )

EGroomCacheAttributes & operator&= ( EGroomCacheAttributes& Lhs, EGroomCacheAttributes Rhs )

EGroomCacheImportType & operator&= ( EGroomCacheImportType& Lhs, EGroomCacheImportType Rhs )

EHairViewRayTracingMask & operator&= ( EHairViewRayTracingMask& Lhs, EHairViewRayTracingMask Rhs )

EGroomBindingAsyncProperties operator^ ( EGroomBindingAsyncProperties Lhs, EGroomBindingAsyncProperties Rhs )

EGroomBindingAsyncPropertyLockType operator^ ( EGroomBindingAsyncPropertyLockType Lhs, EGroomBindingAsyncPropertyLockType Rhs )

EGroomCacheAttributes operator^ ( EGroomCacheAttributes Lhs, EGroomCacheAttributes Rhs )

EGroomCacheImportType operator^ ( EGroomCacheImportType Lhs, EGroomCacheImportType Rhs )

EHairViewRayTracingMask operator^ ( EHairViewRayTracingMask Lhs, EHairViewRayTracingMask Rhs )

EGroomBindingAsyncProperties & operator^= ( EGroomBindingAsyncProperties& Lhs, EGroomBindingAsyncProperties Rhs )

EGroomBindingAsyncPropertyLockType & operator^= ( EGroomBindingAsyncPropertyLockType& Lhs, EGroomBindingAsyncPropertyLockType Rhs )

EGroomCacheAttributes & operator^= ( EGroomCacheAttributes& Lhs, EGroomCacheAttributes Rhs )

EGroomCacheImportType & operator^= ( EGroomCacheImportType& Lhs, EGroomCacheImportType Rhs )

EHairViewRayTracingMask & operator^= ( EHairViewRayTracingMask& Lhs, EHairViewRayTracingMask Rhs )

EGroomBindingAsyncProperties operator| ( EGroomBindingAsyncProperties Lhs, EGroomBindingAsyncProperties Rhs )

EGroomBindingAsyncPropertyLockType operator| ( EGroomBindingAsyncPropertyLockType Lhs, EGroomBindingAsyncPropertyLockType Rhs )

EGroomCacheAttributes operator| ( EGroomCacheAttributes Lhs, EGroomCacheAttributes Rhs )

EGroomCacheImportType operator| ( EGroomCacheImportType Lhs, EGroomCacheImportType Rhs )

EHairViewRayTracingMask operator| ( EHairViewRayTracingMask Lhs, EHairViewRayTracingMask Rhs )

EHairResourceStatus operator| ( EHairResourceStatus In, EHairResourceStatus::EStatus InStatus )

EGroomBindingAsyncProperties & operator|= ( EGroomBindingAsyncProperties& Lhs, EGroomBindingAsyncProperties Rhs )

EGroomBindingAsyncPropertyLockType & operator|= ( EGroomBindingAsyncPropertyLockType& Lhs, EGroomBindingAsyncPropertyLockType Rhs )

EGroomCacheAttributes & operator|= ( EGroomCacheAttributes& Lhs, EGroomCacheAttributes Rhs )

EGroomCacheImportType & operator|= ( EGroomCacheImportType& Lhs, EGroomCacheImportType Rhs )

EHairViewRayTracingMask & operator|= ( EHairViewRayTracingMask& Lhs, EHairViewRayTracingMask Rhs )

EHairResourceStatus & operator|= ( EHairResourceStatus& Out, EHairResourceStatus::EStatus InStatus )

EGroomBindingAsyncProperties operator~ ( EGroomBindingAsyncProperties E )

EGroomBindingAsyncPropertyLockType operator~ ( EGroomBindingAsyncPropertyLockType E )

EGroomCacheAttributes operator~ ( EGroomCacheAttributes E )

EGroomCacheImportType operator~ ( EGroomCacheImportType E )

EHairViewRayTracingMask operator~ ( EHairViewRayTracingMask E )

bool RequestStrandsPosition ( const UGroomComponent* Component, TSharedPtr< FStrandsPositionOutput > Output, const bool bReadGuides )

void SetGroomAttribute ( FHairDescription& HairDescription, FGroomID GroomID, FName AttributeName, AttributeType AttributeValue )

void SetHairAttribute ( uint32& Out, EHairAttribute InAttribute )

void SetHairAttributeFlags ( uint32& Out, EHairAttributeFlags InFlag )

void SetHairStrandAttribute ( FHairDescription& HairDescription, FStrandID StrandID, FName AttributeName, AttributeType AttributeValue )

void SetHairVertexAttribute ( FHairDescription& HairDescription, FVertexID VertexID, FName AttributeName, AttributeType AttributeValue )



---

## HairStrandsDataflow

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HairStrandsDataflow

**Contents:**
- HairStrandsDataflow
- Navigation
- Classes
- Structs
- Enums
  - Public
- Constants
- Variables
  - Public
- Functions

Spline skinning parameter key | BuildGroomSplineSkinningNode.h |

Spline skinning parameter attribute name. | BuildGroomSplineSkinningNode.h |

virtual void Evaluate ( UE::Dataflow::FContext& Context, const FDataflowOutput* Out ) const

virtual void Evaluate ( UE::Dataflow::FContext& Context, const FDataflowOutput* Out ) const

virtual void SetAssetValue ( TObjectPtr< UObject > Asset, UE::Dataflow::FContext& Context ) const



---

## HairStrandsEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HairStrandsEditor

**Contents:**
- HairStrandsEditor
- Navigation
- Classes
- Structs
- Interfaces
- Functions
  - Public

LLM_DECLARE_TAG_API ( GroomEditor )



---

## HairStrandsMutableEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HairStrandsMutableEditor

**Contents:**
- HairStrandsMutableEditor
- Navigation
- Classes



---

## HairStrandsMutable

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HairStrandsMutable

**Contents:**
- HairStrandsMutable
- Navigation
- Classes
- Structs



---

## HairStrandsSolver

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HairStrandsSolver

**Contents:**
- HairStrandsSolver
- Navigation
- Classes
- Structs



---

## HarmonixDspEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HarmonixDspEditor

**Contents:**
- HarmonixDspEditor
- Navigation
- Classes



---

## HarmonixDsp

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HarmonixDsp

**Contents:**
- HarmonixDsp
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

float Harmonix::Dsp::AudioAnalysis::CalculatePSNR ( const T* InterleavedInA, const T* InterleavedInB, const int32 NumChannels, const int32 NumSampleFrames )

float HarmonixDsp::ClampDB ( float dB )

float HarmonixDsp::dBFS ( float Linear )

float HarmonixDsp::DBToLinear ( float dB )

int8 HarmonixDsp::DBToMidiLinear ( float dB )

void HarmonixDsp::FAudioBuffer::Convert ( const TAudioBuffer< float >& Source, TAudioBuffer< int16 >& Destination )

void HarmonixDsp::FAudioBuffer::Convert ( const TAudioBuffer< int16 >& Source, TAudioBuffer< float >& Destination )

void HarmonixDsp::FAudioBuffer::DebugLog ( const int16* InData, uint64 InNumSamples )

void HarmonixDsp::FAudioBuffer::DebugLog ( const float* InData, uint64 InNumSamples )

ESpeakerMask::Type HarmonixDsp::FAudioBuffer::GetChannelMaskForNumChannels ( uint32 NumChannels )

EAudioBufferChannelLayout HarmonixDsp::FAudioBuffer::GetDefaultChannelLayoutForChannelCount ( uint32 ChannelCount )

int32 HarmonixDsp::FAudioBuffer::GetNumChannelsInChannelLayout ( EAudioBufferChannelLayout ChannelLayout )

float HarmonixDsp::FRandSample()

void HarmonixDsp::GenerateWhiteNoiseEq ( T* Output, uint32 NumFrames, float Gain )

float HarmonixDsp::LinearToDB ( float Gain )

float HarmonixDsp::Log10 ( float Value )

double HarmonixDsp::Log10 ( double Value )

float HarmonixDsp::Midi14BitLinearToDB ( int32 Level )

float HarmonixDsp::MidiLinearToDB ( int8 Level )

void HarmonixDsp::PanToGainsConstantPower ( float Pan, float& OutLeftGain, float& OutRightGain )



---

## HarmonixEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HarmonixEditor

**Contents:**
- HarmonixEditor
- Navigation
- Classes



---

## HarmonixMetasoundEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HarmonixMetasoundEditor

**Contents:**
- HarmonixMetasoundEditor
- Navigation
- Classes



---

## HarmonixMetasound

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HarmonixMetasound

**Contents:**
- HarmonixMetasound
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Constants
- Variables
  - Public

DECLARE_METASOUND_DATA_REFERENCE_TYPES ( FMidiEventInfo, FMidiEventInfoTypeInfo, FMidiEventInfoReadRef, FMidiEventInfoWriteRef )

DECLARE_METASOUND_DATA_REFERENCE_TYPES ( FHarmonixFFTAnalyzerResults, HARMONIXMETASOUND_API, FHarmonixFFTAnalyzerResultsTypeInfo, FHarmonixFFTAnalyzerResultsReadRef, FHarmonixFFTAnalyzerResultsWriteRef )

DECLARE_METASOUND_DATA_REFERENCE_TYPES ( FMusicSeekRequest, HARMONIXMETASOUND_API, FMusicSeekRequestTypeInfo, FMusicSeekRequestReadRef, FMusicSeekRequestWriteRef )

DECLARE_METASOUND_DATA_REFERENCE_TYPES ( FTimeSignature, HARMONIXMETASOUND_API, FTimeSignatureTypeInfo, FTimeSignatureReadRef, FTimeSignatureWriteRef )

HarmonixMetasound::Analysis::DECLARE_METASOUND_DATA_REFERENCE_ALIAS_TYPES ( FMidiClockSongPosition, FMidiClockSongPositionTypeInfo, FMidiClockSongPositionReadRef, FMidiClockSongPositionWriteRef )

HarmonixMetasound::DECLARE_METASOUND_DATA_REFERENCE_ALIAS_TYPES ( FMidiClock, FMidiClockTypeInfo, FMidiClockReadRef, FMidiClockWriteRef )

HarmonixMetasound::DECLARE_METASOUND_DATA_REFERENCE_ALIAS_TYPES ( FMusicTransportEvent, FMusicTransportEventTypeInfo, FMusicTransportEventReadRef, FMusicTransportEventWriteRef )

DECLARE_METASOUND_DATA_REFERENCE_ALIAS_TYPES(FMusicTransportEventStream, FMusicTransportEventStreamTypeInfo, FMusicTransportEventStreamReadRef, FMusicTransportEventStreamWriteRef) enum class EMusicPlayerTransportState FString HarmonixMetasound::MusicPlayerTransportStateToString ( EMusicPlayerTransportState State )

const Metasound::FNodeClassName & HarmonixMetasound::Nodes::MorphingLFO::GetClassName()

const Metasound::FNodeClassName & HarmonixMetasound::Nodes::MusicTimeStampToSeekTarget::GetClassName()

int32 HarmonixMetasound::Nodes::MusicTimeStampToSeekTarget::GetCurrentMajorVersion()

void MusicTempometerUtilities::UpdateMaterialParameterCollectionFromClock ( const UObject* InWorldContextObject, TWeakObjectPtr< UMaterialParameterCollectionInstance >& InOutMaterialParameterCollectionInstance, const TObjectPtr< UMaterialParameterCollection >& InMaterialParameterCollection, const FMusicTempometerMPCParameters& InMCPParameters, const UMusicClockComponent* InClockComponent )

FMidiSongPos MusicTempometerUtilities::UpdateMaterialParameterCollectionFromClock ( const UMusicClockComponent* InClockComponent, const FMidiSongPos& InPreviousFrameMidiSongPos, const UMaterialParameterCollection* InMaterialParameterCollection, const FMusicTempometerMPCParameters& InMPCParameters, TWeakObjectPtr< UMaterialParameterCollectionInstance >& InOutMaterialParameterCollectionInstance )

void MusicTempometerUtilities::UpdateMaterialParameterCollectionFromSongPos ( const UObject* InWorldContextObject, TWeakObjectPtr< UMaterialParameterCollectionInstance >& InOutMaterialParameterCollectionInstance, const TObjectPtr< UMaterialParameterCollection >& InMaterialParameterCollection, const FMusicTempometerMPCParameters& InMCPParameters, const FMidiSongPos& InMidiSongPos )

void MusicTempometerUtilities::UpdateMaterialParameterCollectionFromSongPos ( const UObject* InWorldContextObject, const FMidiSongPos& InCurrentFrameMidiSongPos, const FMidiSongPos& InPreviousFrameMidiSongPos, const UMaterialParameterCollection* InMaterialParameterCollection, const FMusicTempometerMPCParameters& InMPCParameters, TWeakObjectPtr< UMaterialParameterCollectionInstance >& InOutMaterialParameterCollectionInstance )



---

## HarmonixMidiEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HarmonixMidiEditor

**Contents:**
- HarmonixMidiEditor
- Navigation
- Classes



---

## HarmonixMidi

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HarmonixMidi

**Contents:**
- HarmonixMidi
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

uint32 GetTypeHash ( const FMidiVoiceId& VoiceId )

int32 Harmonix::Midi::Constants::BPMToMidiTempo ( float Bpm )

uint8 Harmonix::Midi::Constants::GetChannel ( uint8 Status )

uint8 Harmonix::Midi::Constants::GetType ( uint8 Status )

bool Harmonix::Midi::Constants::IsChanPres ( uint8 Status )

bool Harmonix::Midi::Constants::IsControl ( uint8 Status )

bool Harmonix::Midi::Constants::IsNoteOff ( uint8 Status )

bool Harmonix::Midi::Constants::IsNoteOn ( uint8 Status )

bool Harmonix::Midi::Constants::IsPitch ( uint8 Status )

bool Harmonix::Midi::Constants::IsPolyPres ( uint8 Status )

bool Harmonix::Midi::Constants::IsProgram ( uint8 Status )

bool Harmonix::Midi::Constants::IsStatus ( uint8 Byte )

bool Harmonix::Midi::Constants::IsSystem ( uint8 Status )

float Harmonix::Midi::Constants::MidiTempoToBPM ( int32 UsPerQuarterNote )

FString MusicalBeatTypeToString ( EMusicalBeatType BeatType )



---

## Harmonix

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Harmonix

**Contents:**
- Harmonix
- Navigation
- Classes
- Structs
- Enums
  - Public
- Constants
- Functions
  - Public

bool Harmonix::CopyStructProperties ( TStructType* InDest, TStructType* InSrc )

bool Harmonix::CopyStructProperty ( TStructType* InDest, TStructType* InSrc, const FPropertyChangedChainEvent& PropertyChangedChainEvent )

bool Harmonix::CopyStructRecursive ( void* InDest, void* InSrc, const UScriptStruct* ScriptStruct )

HARMONIX_APIEPostEditAction Harmonix::GetPropertyPostEditAction ( const FProperty* Property, EPropertyChangeType::Type ChangeType, EPostEditAction DefaultAction )

EPostEditType Harmonix::GetPropertyPostEditType ( const FProperty* Property )

FString Harmonix::GetStructPropertyChainString ( TStructType* StructPtr, const FPropertyChangedChainEvent& PropertyChangedChainEvent )

void Harmonix::LogPropertyValue ( void* PropValuePtr, FProperty* Property )

void Harmonix::LogStructProperties ( TStructType* StructPtr )

void Harmonix::LogStructRecursive ( void* PropPtr, const UScriptStruct* ScriptStruct )



---

## HDRIBackdrop

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HDRIBackdrop

**Contents:**
- HDRIBackdrop
- Navigation
- Classes



---

## HierarchyTableAnimationEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HierarchyTableAnimationEditor

**Contents:**
- HierarchyTableAnimationEditor
- Navigation
- Classes



---

## HierarchyTableAnimationRuntime

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HierarchyTableAnimationRuntime

**Contents:**
- HierarchyTableAnimationRuntime
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## HierarchyTableAnimationUncookedOnly

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HierarchyTableAnimationUncookedO-

**Contents:**
- HierarchyTableAnimationUncookedOnly
- Navigation
- Classes



---

## HierarchyTableEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HierarchyTableEditor

**Contents:**
- HierarchyTableEditor
- Navigation
- Classes
- Structs
- Interfaces



---

## HierarchyTableRuntime

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HierarchyTableRuntime

**Contents:**
- HierarchyTableRuntime
- Navigation
- Classes
- Structs



---

## Hotfix

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Hotfix

**Contents:**
- Hotfix
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

FString LexToString ( EUpdateCompletionStatus Status )



---

## HTNPlanner

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HTNPlanner

**Contents:**
- HTNPlanner
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## HTNTestSuite

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HTNTestSuite

**Contents:**
- HTNTestSuite
- Navigation
- Interfaces



---

## HttpBlueprint

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HttpBlueprint

**Contents:**
- HttpBlueprint
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

bool operator! ( EHttpVerbs E )

EHttpVerbs operator& ( EHttpVerbs Lhs, EHttpVerbs Rhs )

EHttpVerbs & operator&= ( EHttpVerbs& Lhs, EHttpVerbs Rhs )

EHttpVerbs operator^ ( EHttpVerbs Lhs, EHttpVerbs Rhs )

EHttpVerbs & operator^= ( EHttpVerbs& Lhs, EHttpVerbs Rhs )

EHttpVerbs operator| ( EHttpVerbs Lhs, EHttpVerbs Rhs )

EHttpVerbs & operator|= ( EHttpVerbs& Lhs, EHttpVerbs Rhs )

EHttpVerbs operator~ ( EHttpVerbs E )



---

## HTTPChunkInstaller

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/HTTPChunkInstaller

**Contents:**
- HTTPChunkInstaller
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

const TCHAR * ECloudAsyncTaskState::ToString ( ECloudAsyncTaskState::Type EnumVal )



---

## ICVFXTesting

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ICVFXTesting

**Contents:**
- ICVFXTesting
- Navigation
- Classes
- Enums
  - Public



---

## IKRigDeveloper

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/IKRigDeveloper

**Contents:**
- IKRigDeveloper
- Navigation
- Classes



---

## IKRigEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/IKRigEditor

**Contents:**
- IKRigEditor
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## IKRig

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/IKRig

**Contents:**
- IKRig
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Constants
- Functions
  - Public

DECLARE_CYCLE_STAT ( TEXT("IK Retarget Goals"), STAT_IKRetargetGoals, STATGROUP_Anim )

uint32 GetTypeHash ( FIKRigGoal ObjectRef )

void IKRetargetOpUtils::OnRetargetChainRenamed ( TArray< T >& InOutChainSettings, const FName InOldChainName, const FName InNewChainName )

void IKRetargetOpUtils::SynchronizeChainSettingsWithIKRig ( TArray< T >& InOutChainSettings, const FIKRetargetOpBase* InRetargetOp, const bool bSkipUnmappedChains, const bool bSkipNonIKChains )

static FQuat GetRotationFromDeformedPoints ( const TArray< FVector >& InInitialPoints, const TArray< FVector >& InCurrentPoints, FVector& OutInitialCentroid, FVector& OutCurrentCentroid )

static void IKRigDebugRendering::DrawWireCube ( FPrimitiveDrawInterface* PDI, const FTransform& Transform, FLinearColor Color, float Size, float Thickness )



---

## ImagePlate

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ImagePlate

**Contents:**
- ImagePlate
- Navigation
- Classes
- Structs



---

## ImageWidgets

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ImageWidgets

**Contents:**
- ImageWidgets
- Navigation
- Classes
- Structs
- Interfaces



---

## ImgMediaEngine

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ImgMediaEngine

**Contents:**
- ImgMediaEngine
- Navigation
- Classes



---

## ImgMediaFactory

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ImgMediaFactory

**Contents:**
- ImgMediaFactory
- Navigation
- Classes



---

## ImgMedia

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ImgMedia

**Contents:**
- ImgMedia
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

CSV_DECLARE_CATEGORY_MODULE_EXTERN ( ImgMedia )



---

## InEditorDocumentation

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InEditorDocumentation

**Contents:**
- InEditorDocumentation
- Navigation
- Classes
- Typedefs



---

## IngestLiveLinkDevice

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/IngestLiveLinkDevice

**Contents:**
- IngestLiveLinkDevice
- Navigation
- Classes
- Structs



---

## InputBlueprintNodes

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InputBlueprintNodes

**Contents:**
- InputBlueprintNodes
- Navigation
- Classes



---

## InputDebuggingEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InputDebuggingEditor

**Contents:**
- InputDebuggingEditor
- Navigation
- Classes



---

## InputEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InputEditor

**Contents:**
- InputEditor
- Navigation
- Classes



---

## InsightsEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InsightsEditor

**Contents:**
- InsightsEditor
- Navigation
- Interfaces



---

## InstancedActorsEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InstancedActorsEditor

**Contents:**
- InstancedActorsEditor
- Navigation
- Classes



---

## InstancedActorsTestSuite

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InstancedActorsTestSuite

**Contents:**
- InstancedActorsTestSuite
- Navigation
- Interfaces



---

## InstancedActors

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InstancedActors

**Contents:**
- InstancedActors
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Variables
  - Public
- Functions

bool operator! ( EInstancedActorsFragmentFlags E )

EInstancedActorsFragmentFlags operator& ( EInstancedActorsFragmentFlags Lhs, EInstancedActorsFragmentFlags Rhs )

EInstancedActorsFragmentFlags & operator&= ( EInstancedActorsFragmentFlags& Lhs, EInstancedActorsFragmentFlags Rhs )

EInstancedActorsFragmentFlags operator^ ( EInstancedActorsFragmentFlags Lhs, EInstancedActorsFragmentFlags Rhs )

EInstancedActorsFragmentFlags & operator^= ( EInstancedActorsFragmentFlags& Lhs, EInstancedActorsFragmentFlags Rhs )

EInstancedActorsFragmentFlags operator| ( EInstancedActorsFragmentFlags Lhs, EInstancedActorsFragmentFlags Rhs )

EInstancedActorsFragmentFlags & operator|= ( EInstancedActorsFragmentFlags& Lhs, EInstancedActorsFragmentFlags Rhs )

EInstancedActorsFragmentFlags operator~ ( EInstancedActorsFragmentFlags E )

void UE::InstancedActors::Debug::DebugDrawLocation ( const int32& DebugDrawMode, const UWorld* World, const UObject* LogOwner, const CategoryType& CategoryName, ELogVerbosity::Type Verbosity, const FVector& Location, float Size, const FColor& Color, const FmtType& Fmt, Types... Args )

void UE::InstancedActors::Debug::DebugDrawSphere ( const int32& DebugDrawMode, const UWorld* World, const UObject* LogOwner, const CategoryType& CategoryName, ELogVerbosity::Type Verbosity, const FSphere& Sphere, const FColor& Color, const FmtType& Fmt, Types... Args )

void UE::InstancedActors::Debug::DrawDebugSolidBox ( const int32& DebugDrawMode, const UWorld* World, const UObject* LogOwner, const CategoryType& CategoryName, ELogVerbosity::Type Verbosity, const FBox& Box, const FColor& Color, const FmtType& Fmt, Types... Args )

bool UE::InstancedActors::Debug::ShouldDebugDraw ( const int32& DebugDrawMode )

bool UE::InstancedActors::Debug::ShouldVisLog ( const int32& DebugDrawMode )

bool UE::InstancedActors::PassesBoundsTest ( const TBoundsType& QueryBounds, EBoundsTestType BoundsTestType, const FInstancedActorsInstanceHandle& InstanceHandle, const FTransform& InstanceTransform )



---

## InstanceDataObjectFixupTool

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InstanceDataObjectFixupTool

**Contents:**
- InstanceDataObjectFixupTool
- Navigation
- Classes



---

## InteractableInterface

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InteractableInterface

**Contents:**
- InteractableInterface
- Navigation
- Classes
- Structs
- Interfaces



---

## InterchangeCommonParser

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InterchangeCommonParser

**Contents:**
- InterchangeCommonParser
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## InterchangeCommon

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InterchangeCommon

**Contents:**
- InterchangeCommon
- Navigation
- Structs
- Enums
  - Public
- Variables
  - Public
- Functions
  - Public

FString UE::Interchange::USD::MakeBoneNodeUid ( const FString& SkeletonPrimPath, const FString& ConcatBonePath )

FString UE::Interchange::USD::MakeNodeUid ( const FString& NodeUid )

FString UE::Interchange::USD::MakeRootBoneNodeUid ( const FString& SkeletonPrimPath )



---

## InterchangeDispatcher

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InterchangeDispatcher

**Contents:**
- InterchangeDispatcher
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

bool UE::Interchange::operator! ( EWorkerState E )

EWorkerState UE::Interchange::operator& ( EWorkerState Lhs, EWorkerState Rhs )

EWorkerState & UE::Interchange::operator&= ( EWorkerState& Lhs, EWorkerState Rhs )

EWorkerState UE::Interchange::operator^ ( EWorkerState Lhs, EWorkerState Rhs )

EWorkerState & UE::Interchange::operator^= ( EWorkerState& Lhs, EWorkerState Rhs )

EWorkerState UE::Interchange::operator| ( EWorkerState Lhs, EWorkerState Rhs )

EWorkerState & UE::Interchange::operator|= ( EWorkerState& Lhs, EWorkerState Rhs )

EWorkerState UE::Interchange::operator~ ( EWorkerState E )



---

## InterchangeDNA

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InterchangeDNA

**Contents:**
- InterchangeDNA
- Navigation
- Classes



---

## InterchangeEditorPipelines

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InterchangeEditorPipelines

**Contents:**
- InterchangeEditorPipelines
- Navigation
- Classes
- Interfaces



---

## InterchangeEditorUtilities

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InterchangeEditorUtilities

**Contents:**
- InterchangeEditorUtilities
- Navigation
- Classes
- Interfaces



---

## InterchangeEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InterchangeEditor

**Contents:**
- InterchangeEditor
- Navigation
- Classes



---

## InterchangeExport

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InterchangeExport

**Contents:**
- InterchangeExport
- Navigation
- Classes
- Interfaces



---

## InterchangeFactoryNodes

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InterchangeFactoryNodes

**Contents:**
- InterchangeFactoryNodes
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## InterchangeFbxParser

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InterchangeFbxParser

**Contents:**
- InterchangeFbxParser
- Navigation
- Classes



---

## InterchangeImport

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InterchangeImport

**Contents:**
- InterchangeImport
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

TMap< FString, EShadingModel > UE::Interchange::GLTFMaterials::GetMaterialFunctionPathsToShadingModels()

TMap< FString, EShadingModel > UE::Interchange::GLTFMaterials::GetMaterialPathsToShadingModels()

TArray< FString > UE::Interchange::GLTFMaterials::GetRequiredMaterialFunctionPaths()

FText UE::Interchange::MaterialX::Private::FormatFText ( const FText& Text, Args&&... args )

static FText UE::Interchange::MaterialX::Private::FormatFText ( const FText& Text )



---

## InterchangeMessages

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InterchangeMessages

**Contents:**
- InterchangeMessages
- Navigation
- Classes



---

## InterchangeNodes

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InterchangeNodes

**Contents:**
- InterchangeNodes
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Variables
  - Public



---

## InterchangeOpenUSDEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InterchangeOpenUSDEditor

**Contents:**
- InterchangeOpenUSDEditor
- Navigation
- Classes



---

## InterchangeOpenUSDImport

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InterchangeOpenUSDImport

**Contents:**
- InterchangeOpenUSDImport
- Navigation
- Classes



---

## InterchangeOpenVDBImport

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InterchangeOpenVDBImport

**Contents:**
- InterchangeOpenVDBImport
- Navigation
- Classes



---

## InterchangePipelines

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InterchangePipelines

**Contents:**
- InterchangePipelines
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

uint32 GetTypeHash ( EInterchangeMaterialXSettings Key )

bool operator== ( EInterchangeMaterialXSettings Lhs, EInterchangeMaterialXSettings Rhs )

void UE::Interchange::MeshesUtilities::ApplySlotMaterialDependencies ( T& FactoryNode, const TMap< FString, FString >& SlotMaterialDependencies, const UInterchangeBaseNodeContainer& NodeContainer, TMap< FString, FString >* ExistingSlotMaterialDependenciesPtr )

void UE::Interchange::MeshesUtilities::ReorderSlotMaterialDependencies ( T& FactoryNode, const UInterchangeBaseNodeContainer& NodeContainer )



---

## InterchangeTestEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InterchangeTestEditor

**Contents:**
- InterchangeTestEditor
- Navigation
- Classes



---

## InterchangeTests

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/InterchangeTests

**Contents:**
- InterchangeTests
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Functions
  - Public

ENUM_CLASS_FLAGS ( EStaticMeshImportTestGroundTruthBitflags )



---

## IntroTutorials

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/IntroTutorials

**Contents:**
- IntroTutorials
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## IoStoreInsights

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/IoStoreInsights

**Contents:**
- IoStoreInsights
- Navigation
- Structs
- Interfaces
- Enums
  - Public



---

## JsonBlueprintUtilities

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/JsonBlueprintUtilities

**Contents:**
- JsonBlueprintUtilities
- Navigation
- Classes



---

## JsonSerialization

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/JsonSerialization

**Contents:**
- JsonSerialization
- Navigation
- Classes



---

## JWT

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/JWT

**Contents:**
- JWT
- Navigation
- Classes
- Interfaces



---

## LandmassEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LandmassEditor

**Contents:**
- LandmassEditor
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Variables
  - Public



---

## Landmass

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Landmass

**Contents:**
- Landmass
- Navigation
- Structs
- Interfaces
- Enums
  - Public



---

## LandscapePatchEditorOnly

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LandscapePatchEditorOnly

**Contents:**
- LandscapePatchEditorOnly
- Navigation
- Classes



---

## LandscapePatch

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LandscapePatch

**Contents:**
- LandscapePatch
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

void UE::Landscape::PatchUtil::CopyTextureOnRenderThread ( FRHICommandListImmediate& RHICmdList, const FTextureResource& Source, FTextureResource& Destination )

FTransform UE::Landscape::PatchUtil::GetHeightmapToWorld ( const FTransform& InLandscapeTransform )



---

## LauncherChunkInstaller

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LauncherChunkInstaller

**Contents:**
- LauncherChunkInstaller
- Navigation
- Classes



---

## LearningAgentsReplay

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LearningAgentsReplay

**Contents:**
- LearningAgentsReplay
- Navigation
- Classes



---

## LearningAgentsTrainingEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LearningAgentsTrainingEditor

**Contents:**
- LearningAgentsTrainingEditor
- Navigation
- Classes



---

## LearningAgentsTraining

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LearningAgentsTraining

**Contents:**
- LearningAgentsTraining
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## LearningAgents

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LearningAgents

**Contents:**
- LearningAgents
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

uint32 GetTypeHash ( const FLearningAgentsActionSchemaElement& Element )

uint32 GetTypeHash ( const FLearningAgentsActionObjectElement& Element )

uint32 GetTypeHash ( const FLearningAgentsActionModifierElement& Element )

uint32 GetTypeHash ( const FLearningAgentsObservationSchemaElement& Element )

uint32 GetTypeHash ( const FLearningAgentsObservationObjectElement& Element )

bool operator== ( const FLearningAgentsActionSchemaElement& Lhs, const FLearningAgentsActionSchemaElement& Rhs )

bool operator== ( const FLearningAgentsActionObjectElement& Lhs, const FLearningAgentsActionObjectElement& Rhs )

bool operator== ( const FLearningAgentsActionModifierElement& Lhs, const FLearningAgentsActionModifierElement& Rhs )

bool operator== ( const FLearningAgentsObservationSchemaElement& Lhs, const FLearningAgentsObservationSchemaElement& Rhs )

bool operator== ( const FLearningAgentsObservationObjectElement& Lhs, const FLearningAgentsObservationObjectElement& Rhs )



---

## LearningTraining

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LearningTraining

**Contents:**
- LearningTraining
- Navigation
- Classes
- Structs
- Enums
  - Public
- Constants
- Functions
  - Public

bool UE::Learning::operator! ( ESubprocessFlags E )

ESubprocessFlags UE::Learning::operator& ( ESubprocessFlags Lhs, ESubprocessFlags Rhs )

ESubprocessFlags & UE::Learning::operator&= ( ESubprocessFlags& Lhs, ESubprocessFlags Rhs )

ESubprocessFlags UE::Learning::operator^ ( ESubprocessFlags Lhs, ESubprocessFlags Rhs )

ESubprocessFlags & UE::Learning::operator^= ( ESubprocessFlags& Lhs, ESubprocessFlags Rhs )

ESubprocessFlags UE::Learning::operator| ( ESubprocessFlags Lhs, ESubprocessFlags Rhs )

ESubprocessFlags & UE::Learning::operator|= ( ESubprocessFlags& Lhs, ESubprocessFlags Rhs )

ESubprocessFlags UE::Learning::operator~ ( ESubprocessFlags E )

TSharedMemoryArrayView< DimNum, ElementType > UE::Learning::SharedMemory::Allocate ( const TLearningArrayShape< DimNum >& Shape )

void UE::Learning::SharedMemory::Deallocate ( TSharedMemoryArrayView< DimNum, ElementType >& Memory )

TSharedMemoryArrayView< DimNum, ElementType > UE::Learning::SharedMemory::Map ( const FGuid Guid, const TLearningArrayShape< DimNum >& Shape, const bool bCreate )

void UE::Learning::SharedMemory::Unmap ( TSharedMemoryArrayView< DimNum, ElementType >& Memory )



---

## Learning

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Learning

**Contents:**
- Learning
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Variables
  - Public
- Functions

void UE::Learning::Array::Check ( const TLearningArrayView< InDimNum, InElementType > View )

void UE::Learning::Array::Check ( const TLearningArray< InDimNum, InElementType, Allocator >& View )

void UE::Learning::Array::Check ( const TLearningArrayView< InDimNum, InElementType > View, const FIndexSet Indices )

void UE::Learning::Array::Check ( const TLearningArray< InDimNum, InElementType >& View, const FIndexSet Indices )

void UE::Learning::Array::CheckShapesEqual ( const TLearningArrayShape< InDimNum >& Lhs, const TLearningArrayShape< InDimNum >& Rhs )

void UE::Learning::Array::Copy ( TLearningArrayView< InDimNum, InElementType > Dst, TLearningArrayView< InDimNum, InElementType > Src )

void UE::Learning::Array::Copy ( TLearningArray< InDimNum, InElementType, Allocator >& Dst, const TLearningArrayView< InDimNum, const InElementType > Src )

void UE::Learning::Array::Copy ( TLearningArrayView< InDimNum, InElementType > Dst, const TLearningArray< InDimNum, InElementType, Allocator >& Src )

void UE::Learning::Array::Copy ( TLearningArray< InDimNum, InElementType, AllocatorLhs >& Dst, const TLearningArray< InDimNum, InElementType, AllocatorRhs >& Src )

void UE::Learning::Array::Copy ( TLearningArrayView< InDimNum, InElementType > Dst, const TLearningArrayView< InDimNum, const InElementType > Src, const FIndexSet Indices )

void UE::Learning::Array::Copy ( TLearningArrayView< InDimNum, InElementType > Dst, const TLearningArray< InDimNum, InElementType, Allocator >& Src, const FIndexSet Indices )

void UE::Learning::Array::Copy ( TLearningArray< InDimNum, InElementType, AllocatorLhs >& Dst, const TLearningArray< InDimNum, InElementType, AllocatorRhs >& Src, const FIndexSet Indices )

void UE::Learning::Array::Copy ( TLearningArray< InDimNum, InElementType, Allocator >& Dst, const TLearningArrayView< InDimNum, const InElementType > Src, const FIndexSet Indices )

void UE::Learning::Array::DeserializeFromBytes32 ( int64& InOutOffset, TLearningArrayView< 1, const uint8 > Bytes, TArray< InElementType, Allocator >& OutArray )

void UE::Learning::Array::DeserializeFromBytes32 ( int64& InOutOffset, TLearningArrayView< 1, const uint8 > Bytes, TLearningArray< InDimNum, InElementType, Allocator >& OutArray )

bool UE::Learning::Array::Equal ( const TLearningArray< InDimNum, InElementType, AllocatorLhs >& Lhs, const TLearningArray< InDimNum, InElementType, AllocatorRhs >& Rhs )

bool UE::Learning::Array::Equal ( const TLearningArrayView< InDimNum, const InElementType > Lhs, const TLearningArray< InDimNum, InElementType, AllocatorRhs >& Rhs )

bool UE::Learning::Array::Equal ( const TLearningArray< InDimNum, InElementType, AllocatorLhs >& Lhs, const TLearningArrayView< InDimNum, const InElementType >& Rhs )

bool UE::Learning::Array::Equal ( const TLearningArrayView< InDimNum, const InElementType > Lhs, const TLearningArrayView< InDimNum, const InElementType > Rhs )

FString UE::Learning::Array::Format ( const TLearningArrayView< 1, const InElementType > Array, const TFunctionRef< FString(const InElementType&)> Formatter, const int32 MaxItemNum )

int64 UE::Learning::Array::IndexOf ( const TLearningArrayView< 1, const InElementType > Array, const InElementType& Element )

int64 UE::Learning::Array::IndexOf ( const TLearningArray< 1, InElementType >& Array, const InElementType& Element )

int32 UE::Learning::Array::SerializationByteNum32 ( const TLearningArrayShape< InDimNum > Shape )

void UE::Learning::Array::Serialize ( FArchive& Ar, TLearningArray< InDimNum, InElementType, Allocator >& Array )

void UE::Learning::Array::SerializeToBytes32 ( int64& InOutOffset, TLearningArrayView< 1, uint8 > Bytes, const TLearningArray< InDimNum, InElementType, Allocator >& InArray )

void UE::Learning::Array::SerializeToBytes32 ( int64& InOutOffset, TLearningArrayView< 1, uint8 > Bytes, const TMultiArrayShape< InDimNum > Shape, const TArray< InElementType, Allocator >& InArray )

void UE::Learning::Array::Set ( TLearningArrayView< InDimNum, InElementType > View, const InElementType& Element )

void UE::Learning::Array::Set ( TLearningArray< InDimNum, InElementType, Allocator >& View, const InElementType& Element )

void UE::Learning::Array::Set ( TLearningArrayView< InDimNum, InElementType > View, const InElementType& Element, const FIndexSet Indices )

void UE::Learning::Array::Set ( TLearningArray< InDimNum, InElementType, Allocator >& View, const InElementType& Element, const FIndexSet Indices )

void UE::Learning::Array::ShiftLeft ( TLearningArray< InDimNum, InElementType, Allocator >& Array, const int64 ShiftNum )

void UE::Learning::Array::ShiftLeft ( TLearningArray< 1, InElementType, Allocator >& Array, const int64 ShiftNum )

void UE::Learning::Array::ShiftLeft ( TLearningArrayView< InDimNum, InElementType > Array, const int64 ShiftNum )

void UE::Learning::Array::ShiftLeft ( TLearningArrayView< 1, InElementType > Array, const int64 ShiftNum )

void UE::Learning::Array::Zero ( TLearningArrayView< InDimNum, InElementType > View )

void UE::Learning::Array::Zero ( TLearningArray< InDimNum, InElementType, Allocator >& Array )

void UE::Learning::Array::Zero ( TLearningArrayView< InDimNum, InElementType > View, const FIndexSet Indices )

void UE::Learning::Array::Zero ( TLearningArray< InDimNum, InElementType, Allocator >& View, const FIndexSet Indices )

void UE::Learning::FrameSet::ParallelForEachFrame ( const FFrameSet& FrameSet, const TFunctionRef< void(const int32 TotalFrameIdx, const int32 EntryIdx, const int32 RangeIdx)> Bod... )

decltype(auto) UE::MultiArrayView::Private::GetDataHelper ( T&& Arg )

decltype(auto) UE::MultiArrayView::Private::GetReinterpretedDataHelper ( T&& Arg )

static FString UE::Learning::Array::FormatFloat ( const TLearningArrayView< 1, const float > Array, const int32 MaxItemNum )

static FString UE::Learning::Array::FormatInt32 ( const TLearningArrayView< 1, const int32 > Array, const int32 MaxItemNum )

static FString UE::Learning::Array::FormatUint64 ( const TLearningArrayView< 1, const uint64 > Array, const int32 MaxItemNum )

static void UE::Learning::DeserializeFromBytes ( int64& InOutOffset, TLearningArrayView< 1, const uint8 > Bytes, uint8& OutValue )

static void UE::Learning::DeserializeFromBytes ( int64& InOutOffset, TLearningArrayView< 1, const uint8 > Bytes, int32& OutValue )

static void UE::Learning::DeserializeFromBytes ( int64& InOutOffset, TLearningArrayView< 1, const uint8 > Bytes, int64& OutValue )

static void UE::Learning::DeserializeFromBytes ( int64& InOutOffset, TLearningArrayView< 1, const uint8 > Bytes, uint64& OutValue )

static void UE::Learning::SerializeToBytes ( int64& InOutOffset, TLearningArrayView< 1, uint8 > Bytes, const uint8 InValue )

static void UE::Learning::SerializeToBytes ( int64& InOutOffset, TLearningArrayView< 1, uint8 > Bytes, const int32 InValue )

static void UE::Learning::SerializeToBytes ( int64& InOutOffset, TLearningArrayView< 1, uint8 > Bytes, const int64 InValue )



---

## LedWallCalibration

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LedWallCalibration

**Contents:**
- LedWallCalibration
- Navigation
- Classes
- Structs



---

## LensComponentEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LensComponentEditor

**Contents:**
- LensComponentEditor
- Navigation
- Classes



---

## LensComponent

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LensComponent

**Contents:**
- LensComponent
- Navigation
- Classes
- Typedefs
- Enums
  - Public



---

## LensDistortion

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LensDistortion

**Contents:**
- LensDistortion
- Navigation
- Classes
- Structs
- Interfaces



---

## LevelSequenceEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LevelSequenceEditor

**Contents:**
- LevelSequenceEditor
- Navigation
- Classes
- Structs
- Interfaces



---

## LevelSnapshotFilters

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LevelSnapshotFilters

**Contents:**
- LevelSnapshotFilters
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Static

static bool EFilterResult::CanInclude ( EFilterResult::Type Type )

static bool EFilterResult::CanNegate ( EFilterResult::Type Type )

static EFilterResult::Type EFilterResult::Negate ( EFilterResult::Type Type )

static bool EFilterResult::ShouldInclude ( EFilterResult::Type Type )



---

## LevelSnapshotsEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LevelSnapshotsEditor

**Contents:**
- LevelSnapshotsEditor
- Navigation
- Classes



---

## LevelSnapshots

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LevelSnapshots

**Contents:**
- LevelSnapshots
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

bool operator! ( ESnapshotClassFlags E )

ESnapshotClassFlags operator& ( ESnapshotClassFlags Lhs, ESnapshotClassFlags Rhs )

ESnapshotClassFlags & operator&= ( ESnapshotClassFlags& Lhs, ESnapshotClassFlags Rhs )

ESnapshotClassFlags operator^ ( ESnapshotClassFlags Lhs, ESnapshotClassFlags Rhs )

ESnapshotClassFlags & operator^= ( ESnapshotClassFlags& Lhs, ESnapshotClassFlags Rhs )

ESnapshotClassFlags operator| ( ESnapshotClassFlags Lhs, ESnapshotClassFlags Rhs )

ESnapshotClassFlags & operator|= ( ESnapshotClassFlags& Lhs, ESnapshotClassFlags Rhs )

ESnapshotClassFlags operator~ ( ESnapshotClassFlags E )

bool UE::LevelSnapshots::AreNumericPropertiesNearlyEqual ( const FNumericProperty* Property, const void* ValuePtrA, const void* ValuePtrB )

FOodleDataCompression::ECompressionLevel UE::LevelSnapshots::Compression::CastCompressionLevel ( ESnapshotCompressionLevel Value )

FOodleDataCompression::ECompressor UE::LevelSnapshots::Compression::CastCompressor ( ESnapshotCompressor Value )

FProperty * UE::LevelSnapshots::GetParentProperty ( const FProperty* Property )

bool UE::LevelSnapshots::IsPropertyCollection ( const FProperty* Property )

bool UE::LevelSnapshots::IsPropertyComponentOrSubobject ( const FProperty* Property )

bool UE::LevelSnapshots::IsPropertyContainer ( const FProperty* Property )

bool UE::LevelSnapshots::IsPropertyInCollection ( const FProperty* Property )

bool UE::LevelSnapshots::IsPropertyInContainer ( const FProperty* Property )

bool UE::LevelSnapshots::IsPropertyInMap ( const FProperty* Property )

bool UE::LevelSnapshots::IsPropertyInStruct ( const FProperty* Property )

bool UE::LevelSnapshots::Restorability::IsActorDesirableForCapture ( const AActor* Actor )

bool UE::LevelSnapshots::Restorability::IsActorRestorable ( const AActor* Actor )

bool UE::LevelSnapshots::Restorability::IsComponentDesirableForCapture ( const UActorComponent* Component )

bool UE::LevelSnapshots::Restorability::IsPropertyDesirableForCapture ( const FProperty* Property )

bool UE::LevelSnapshots::Restorability::IsPropertyExplicitlySupportedForCapture ( const FProperty* Property )

bool UE::LevelSnapshots::Restorability::IsPropertyExplicitlyUnsupportedForCapture ( const FProperty* Property )

bool UE::LevelSnapshots::Restorability::IsRestorableProperty ( const FProperty* LeafProperty )

bool UE::LevelSnapshots::Restorability::IsSubobjectClassDesirableForCapture ( const UClass* SubobjectClass )

bool UE::LevelSnapshots::Restorability::IsSubobjectDesirableForCapture ( const UObject* Subobject )

bool UE::LevelSnapshots::Restorability::ShouldConsiderMatchedActorForRestoration ( const FCanModifyMatchedActorParams& Params, FText* ExclusionReason )

bool UE::LevelSnapshots::Restorability::ShouldConsiderNewActorForRemoval ( const AActor* Actor, FText* ExclusionReason )

bool UE::LevelSnapshots::Restorability::ShouldConsiderRemovedActorForRecreation ( const FCanRecreateActorParams& Params, FText* ExclusionReason )

void UE::LevelSnapshots::UpdateDecimalComparisionPrecision ( float FloatPrecision, double DoublePrecision )



---

## LevelStreamingPersistence

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LevelStreamingPersistence

**Contents:**
- LevelStreamingPersistence
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## Level Editor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/level-editor-in-unreal-engine

**Contents:**
- Level Editor
- The Default Interface
  - Tab Bar
  - Toolbar
  - Menu Bar
  - Modes
  - Viewport
  - Details
  - Outliner
  - Bottom Toolbar

An overview of the interface used for the design and construction of game levels and environments.

The Level Editor provides the core level creation functionality for Unreal Editor. You will use it to create, view, and modify levels .You will modify a level mainly by placing, transforming, and editing the properties of Actors.

In Unreal Editor, the scenes in which you create your game experience are generally referred to as Levels. You can think of a level as a 3D environment into which you place a series of objects and geometry to define the world your players will experience. Any object that is placed in your world, be it a light, a mesh, or a character, is considered to be an Actor. Technically speaking, an Actor is a programming class used within the Unreal Engine to define an object that has 3D position, rotation, and scale data. Think of an Actor as any object that can be placed in your levels.

Click image for full size.

Creating levels begins by placing items in a map inside Unreal Editor. These items may be world geometry, decorations in the form of Brushes, Static Meshes, lights, player starts, weapons, or vehicles. Which items are added when is usually defined by the particular workflow used by the level design team.

Since the interface for Unreal Editor is highly customizable, it is possible that what you see may change from one launch to the next. Below, you can see the default interface layout.

Click image for full size.

The Level Editor has a tab along the top with the name of the current level. Tabs from other editor windows may be docked alongside this tab for quick and easy navigation, similar to a web browser.

Click image for full size.

The name of the tab reflects the level currently being edited. This is a pattern consistent throughout the editor—tabs will be named after the current asset being edited.

To the right of the Tab Bar is the name of the current project.

Click image for full size.

The Toolbar panel displays a group of commands, providing quick access to commonly used tools and operations.

See the Toolbar page for descriptions Toolbar items.

The Menu Bar in the editor should be familiar to anyone who has used Windows applications previously. It provides access to general tools and commands that are used when working with levels in the editor.

Click image for full size.

The Console (`) is a text field that allows special console commands to be entered that are recognized by the editor. The text field has an auto-complete feature that automatically lists all commands matching the characters in the field.

If are running Source Control, the button on the far right of the menu bar is indicates its status.

The Level Editor can be put into different editing modes to enable specialized editing interfaces and workflows for editing particular types of Actors or geometry.

To display a selection of modes, in the Level Editor Toolbar, open the Modes dropdown.

Click image for full size.

Modes change the primary behavior of the Level Editor for a specialized task, such as moving and transforming assets in the world, sculpting landscapes, generating foliage, creating geometry brushes and volumes, and painting on meshes. Modes panels contain a selection of tools tailored to the selected editing mode.

Click image for full size.

You can close any panel by clicking the small "X" in the upper-right corner of the tab. You can also hide any panel by right-clicking on the tab, and then clicking Hide Tab on the context menu that appears. To reopen a panel that you have closed, click that panel's name on the Window menu.

The Viewport panel is your window into the worlds you create in Unreal Engine.

Click image for full size.

This panel contains a set of viewports, each of which can be maximized to fill the entire panel and offer the ability to display the world from one of three orthographic views (Top, Side, Front) or a perspective view giving you complete control over what you see and how you see it.

See Viewports for more information on working with viewports.

Click image for full size.

The Details panel contains information, utilities, and functions for the current selection in the viewport. It contains transform edit boxes for moving, rotating, and scaling Actors, displays all of the editable properties for the selected Actors, and provides quick access to additional editing functionality depending on the type of Actor(s) selected in the viewport. For example, selected Actors can be exported to FBX and converted to another compatible type. Selection Details allow you to view the materials used by the selected Actors, if any, and quickly open them for editing.

See the Details page for a more complete overview and guide to using the Details panel in the Level Editor.

Click image for full size.

The Outliner panel displays all of the Actors within the scene in a hierarchical tree view. You can select and modify Actors directly from the Outliner. Use the Info dropdown menu to display an additional column that shows Levels, Layers, or ID Names.

See the Outliner page for details on using the Outliner.

Click image for full size.

Contains shortcuts to the Command Console, Output Log, and Derived Data functionality. Also displays source control status.

See the Toolbar page for descriptions Toolbar items.

The Layers panel allows you to organize Actors in your Level.

Click image for full size.

Layers provide the ability to quickly select as well as control visibility of groups of related Actors. You can use your layers to quickly un-clutter a scene leaving only the geometry and Actors that you are working with. For example, you might be working on a building that has multiple levels but is comprised of many modular parts. By assigning each floor to a layer, you can hide each of the floors you are not working on making the top view much more manageable.

See the Layers Panel page for details on using the Layers panel.



---

## LibVpxCodecs

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LibVpxCodecs

**Contents:**
- LibVpxCodecs
- Navigation
- Classes
- Structs



---

## LidarPointCloudEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LidarPointCloudEditor

**Contents:**
- LidarPointCloudEditor
- Navigation
- Interfaces



---

## LidarPointCloudRuntime

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LidarPointCloudRuntime

**Contents:**
- LidarPointCloudRuntime
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Variables
  - Public
- Functions

void LidarPointCloudMeshing::BuildCollisionMesh ( FLidarPointCloudOctree* Octree, const float& CellSize, FTriMeshCollisionData* CollisionMesh )

void LidarPointCloudMeshing::BuildStaticMeshBuffers ( FLidarPointCloudOctree* Octree, const float& CellSize, bool bUseSelection, FMeshBuffers* OutMeshBuffers, const FTransform& Transform )

void LidarPointCloudMeshing::CalculateNormals ( FLidarPointCloudOctree* Octree, FThreadSafeBool* bCancelled, int32 Quality, float Tolerance, TArray64< FLidarPointCloudPoint* >& InPointSelection )



---

## LightGizmos

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LightGizmos

**Contents:**
- LightGizmos
- Navigation
- Classes



---

## LightMixer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LightMixer

**Contents:**
- LightMixer
- Navigation
- Classes



---

## LightWeightInstancesEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LightWeightInstancesEditor

**Contents:**
- LightWeightInstancesEditor
- Navigation
- Classes



---

## LinearTimecode

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LinearTimecode

**Contents:**
- LinearTimecode
- Navigation
- Classes
- Structs



---

## LiveLinkCamera

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkCamera

**Contents:**
- LiveLinkCamera
- Navigation
- Classes
- Structs



---

## LiveLinkCapabilities

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkCapabilities

**Contents:**
- LiveLinkCapabilities
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

bool operator! ( EIngestCapability_ProcessConfig E )

EIngestCapability_ProcessConfig operator& ( EIngestCapability_ProcessConfig Lhs, EIngestCapability_ProcessConfig Rhs )

EIngestCapability_ProcessConfig & operator&= ( EIngestCapability_ProcessConfig& Lhs, EIngestCapability_ProcessConfig Rhs )

EIngestCapability_ProcessConfig operator^ ( EIngestCapability_ProcessConfig Lhs, EIngestCapability_ProcessConfig Rhs )

EIngestCapability_ProcessConfig & operator^= ( EIngestCapability_ProcessConfig& Lhs, EIngestCapability_ProcessConfig Rhs )

EIngestCapability_ProcessConfig operator| ( EIngestCapability_ProcessConfig Lhs, EIngestCapability_ProcessConfig Rhs )

EIngestCapability_ProcessConfig & operator|= ( EIngestCapability_ProcessConfig& Lhs, EIngestCapability_ProcessConfig Rhs )

EIngestCapability_ProcessConfig operator~ ( EIngestCapability_ProcessConfig E )



---

## LiveLinkComponents

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkComponents

**Contents:**
- LiveLinkComponents
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## LiveLinkControlRig

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkControlRig

**Contents:**
- LiveLinkControlRig
- Navigation
- Classes
- Structs
- Functions
  - Public
  - Static

C void IMPLEMENT_MODULE_LiveLinkControlRig()

ILiveLinkClient * LiveLinkControlRigUtilities::TryGetLiveLinkClient()

static IModuleInterface * InitializeLiveLinkControlRigModule()

static FModuleInitializerEntry LiveLinkControlRigInitializerEntry ( TEXT("LiveLinkControlRig"), InitializeLiveLinkControlRigModule, TEXT(UE_MODULE_NAME) )



---

## LiveLinkCurveDebugUI

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkCurveDebugUI

**Contents:**
- LiveLinkCurveDebugUI
- Navigation
- Classes
- Interfaces



---

## LiveLinkDevice

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkDevice

**Contents:**
- LiveLinkDevice
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

DECLARE_TS_MULTICAST_DELEGATE_OneParam ( FDeviceConnectionStatusChanged, ELiveLinkDeviceConnectionStatus )



---

## LiveLinkEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkEditor

**Contents:**
- LiveLinkEditor
- Navigation
- Classes
- Structs
- Typedefs



---

## LiveLinkFaceDiscovery

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkFaceDiscovery

**Contents:**
- LiveLinkFaceDiscovery
- Navigation
- Classes



---

## LiveLinkFaceMetadata

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkFaceMetadata

**Contents:**
- LiveLinkFaceMetadata
- Navigation



---

## LiveLinkFaceSource

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkFaceSource

**Contents:**
- LiveLinkFaceSource
- Navigation
- Classes



---

## LiveLinkFreeD

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkFreeD

**Contents:**
- LiveLinkFreeD
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## LiveLinkGraphNode

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkGraphNode

**Contents:**
- LiveLinkGraphNode
- Navigation
- Classes



---

## LiveLinkHubCaptureMessaging

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkHubCaptureMessaging

**Contents:**
- LiveLinkHubCaptureMessaging
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## LiveLinkHubEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkHubEditor

**Contents:**
- LiveLinkHubEditor
- Navigation
- Structs
- Functions
  - Public

bool UE::LiveLinkHubLauncherUtils::FindLiveLinkHubInstallation ( FInstalledApp& OutLiveLinkHubInfo )

void UE::LiveLinkHubLauncherUtils::OpenLiveLinkHub()



---

## LiveLinkHubExportServer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkHubExportServer

**Contents:**
- LiveLinkHubExportServer
- Navigation
- Classes



---

## LiveLinkHubMessaging

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkHubMessaging

**Contents:**
- LiveLinkHubMessaging
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## LiveLinkHubWorkerManager

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkHubWorkerManager

**Contents:**
- LiveLinkHubWorkerManager
- Navigation
- Classes



---

## LiveLinkHub

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkHub

**Contents:**
- LiveLinkHub
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Constants
- Variables
  - Public
- Functions

FLiveLinkHubComponentInitParams ( TSharedRef< SWindow > InWindow, TSharedRef< FTabManager::FStack > InMainStack )



---

## LiveLinkInputDevice

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkInputDevice

**Contents:**
- LiveLinkInputDevice
- Navigation
- Classes
- Structs



---

## LiveLinkLens

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkLens

**Contents:**
- LiveLinkLens
- Navigation
- Classes
- Structs



---

## LiveLinkMasterLockit

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkMasterLockit

**Contents:**
- LiveLinkMasterLockit
- Navigation
- Classes
- Structs



---

## LiveLinkMovieScene

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkMovieScene

**Contents:**
- LiveLinkMovieScene
- Navigation
- Classes
- Structs
- Interfaces
- Functions
  - Public

void MovieSceneLiveLinkSectionUtils::CreateChannelEditor ( const FText& InDisplayName, ChannelType& InChannel, int32 InChannelIndex, ExtendedEditorDataType&& InExtendedEditorDataType, TArray< bool >& OutChannelMask, FMovieSceneChannelProxyData& OutChannelData )



---

## LiveLinkOpenTrackIO

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkOpenTrackIO

**Contents:**
- LiveLinkOpenTrackIO
- Navigation
- Classes
- Enums
  - Public



---

## LiveLinkOverNDisplay

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkOverNDisplay

**Contents:**
- LiveLinkOverNDisplay
- Navigation
- Classes
- Interfaces



---

## LiveLinkPrestonMDR

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkPrestonMDR

**Contents:**
- LiveLinkPrestonMDR
- Navigation
- Classes
- Structs



---

## LiveLinkSequencer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkSequencer

**Contents:**
- LiveLinkSequencer
- Navigation
- Classes



---

## LiveLinkVRPN

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkVRPN

**Contents:**
- LiveLinkVRPN
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## LiveLinkXR

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLinkXR

**Contents:**
- LiveLinkXR
- Navigation
- Classes
- Structs



---

## LiveLink

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveLink

**Contents:**
- LiveLink
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

void LiveLinkBlueprintStructsHeaderDeprecatedWarning()

void TriggerLiveLinkBlueprintStructsHeaderDeprecatedWarning()



---

## LiveUpdateForSlate

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LiveUpdateForSlate

**Contents:**
- LiveUpdateForSlate
- Navigation
- Classes



---

## Lobby

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Lobby

**Contents:**
- Lobby
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## LocalizableMessageBlueprint

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LocalizableMessageBlueprint

**Contents:**
- LocalizableMessageBlueprint
- Navigation
- Classes



---

## LocalizableMessage

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LocalizableMessage

**Contents:**
- LocalizableMessage
- Navigation
- Classes
- Structs
- Interfaces



---

## LocationServicesBPLibrary

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LocationServicesBPLibrary

**Contents:**
- LocationServicesBPLibrary
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## Locomotor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Locomotor

**Contents:**
- Locomotor
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## LoginFlow

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/LoginFlow

**Contents:**
- LoginFlow
- Navigation
- Classes
- Interfaces
- Typedefs
- Enums
  - Public



---

## MassActors

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassActors

**Contents:**
- MassActors
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

bool UE::MassActor::AddEntityTagToActor ( const AActor& Actor )

bool UE::MassActor::RemoveEntityTagFromActor ( const AActor& Actor )



---

## MassAIBehavior

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassAIBehavior

**Contents:**
- MassAIBehavior
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

static EProcessorExecutionFlags UE::MassStateTree::ExecutionFlags ( EProcessorExecutionFlags::Standalone|EProcessorExecutionFlags::Server )



---

## MassAIDebug

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassAIDebug

**Contents:**
- MassAIDebug
- Navigation
- Classes
- Interfaces



---

## MassAIReplication

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassAIReplication

**Contents:**
- MassAIReplication
- Navigation
- Classes
- Structs
- Interfaces



---

## MassAITestSuite

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassAITestSuite

**Contents:**
- MassAITestSuite
- Navigation
- Interfaces



---

## MassCommon

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassCommon

**Contents:**
- MassCommon
- Navigation
- Classes
- Structs
- Interfaces
- Variables
  - Public
- Functions
  - Public

uint32 UE::RandomSequence::FibocciHash ( const int32 SeqIndex )

uint32 UE::RandomSequence::FibonacciHash ( const int32 SeqIndex )

float UE::RandomSequence::FRand ( const int32 SeqIndex )

float UE::RandomSequence::FRandRange ( const int32 SeqIndex, const float InMin, const float InMax )

int32 UE::RandomSequence::RandHelper ( const int32 SeqIndex, const int32 A )

int32 UE::RandomSequence::RandRange ( const int32 SeqIndex, const int32 InMin, const int32 InMax )

float UE::RandomSequence::RandRange ( const int32 SeqIndex, const float InMin, const float InMax )



---

## MassCrowd

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassCrowd

**Contents:**
- MassCrowd
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## MassEQS

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassEQS

**Contents:**
- MassEQS
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## MassGameplayDebug

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassGameplayDebug

**Contents:**
- MassGameplayDebug
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## MassGameplayEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassGameplayEditor

**Contents:**
- MassGameplayEditor
- Navigation
- Classes
- Structs
- Interfaces



---

## MassGameplayExternalTraits

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassGameplayExternalTraits

**Contents:**
- MassGameplayExternalTraits
- Navigation
- Interfaces



---

## MassGameplayTestSuite

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassGameplayTestSuite

**Contents:**
- MassGameplayTestSuite
- Navigation
- Interfaces



---

## MassInsightsAnalysis

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassInsightsAnalysis

**Contents:**
- MassInsightsAnalysis
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## MassMovementEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassMovementEditor

**Contents:**
- MassMovementEditor
- Navigation
- Classes
- Interfaces
- Functions
  - Public

TOptional< T > UE::MassMovement::PropertyUtils::GetValue ( const TSharedPtr< IPropertyHandle >& ValueProperty )

void UE::MassMovement::PropertyUtils::SetValue ( TSharedPtr< IPropertyHandle >& ValueProperty, T NewValue, EPropertyValueSetFlags::Type Flags )



---

## MassMovement

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassMovement

**Contents:**
- MassMovement
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## MassNavigationEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassNavigationEditor

**Contents:**
- MassNavigationEditor
- Navigation
- Classes
- Interfaces



---

## MassNavigation

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassNavigation

**Contents:**
- MassNavigation
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

bool operator! ( EMassNavigationObstacleFlags E )

EMassNavigationObstacleFlags operator& ( EMassNavigationObstacleFlags Lhs, EMassNavigationObstacleFlags Rhs )

EMassNavigationObstacleFlags & operator&= ( EMassNavigationObstacleFlags& Lhs, EMassNavigationObstacleFlags Rhs )

EMassNavigationObstacleFlags operator^ ( EMassNavigationObstacleFlags Lhs, EMassNavigationObstacleFlags Rhs )

EMassNavigationObstacleFlags & operator^= ( EMassNavigationObstacleFlags& Lhs, EMassNavigationObstacleFlags Rhs )

EMassNavigationObstacleFlags operator| ( EMassNavigationObstacleFlags Lhs, EMassNavigationObstacleFlags Rhs )

EMassNavigationObstacleFlags & operator|= ( EMassNavigationObstacleFlags& Lhs, EMassNavigationObstacleFlags Rhs )

EMassNavigationObstacleFlags operator~ ( EMassNavigationObstacleFlags E )

FVector UE::MassNavigation::ClampVector ( const FVector Vec, const FVector::FReal Mag )

FVector UE::MassNavigation::ComputeMiterNormal ( const FVector NormalA, const FVector NormalB )

bool UE::MassNavigation::Debug::DebugIsSelected ( const FMassEntityHandle Entity )

FColor UE::MassNavigation::Debug::MixColors ( const FColor ColorA, const FColor ColorB )

FVector::FReal UE::MassNavigation::ExponentialSmoothingAngle ( const FVector::FReal Angle, const FVector::FReal TargetAngle, const FVector::FReal DeltaTime, const FVector::FReal SmoothingTime )

FVector UE::MassNavigation::GetLeftDirection ( const FVector Forward, const FVector Up )

FVector::FReal UE::MassNavigation::GetYawFromDirection ( const FVector Direction )

FQuat::FReal UE::MassNavigation::GetYawFromQuat ( const FQuat Rotation )

FVector::FReal UE::MassNavigation::LerpAngle ( const FVector::FReal AngleA, const FVector::FReal AngleB, const FVector::FReal T )

FVector::FReal UE::MassNavigation::ProjectPtSeg ( const FVector2D Point, const FVector2D Start, const FVector2D End )

float UE::MassNavigation::Smooth ( const float X )

double UE::MassNavigation::Smooth ( const double X )

FVector::FReal UE::MassNavigation::WrapAngle ( const FVector::FReal Angle )



---

## MassNavMeshNavigation

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassNavMeshNavigation

**Contents:**
- MassNavMeshNavigation
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## MassReplication

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassReplication

**Contents:**
- MassReplication
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Variables
  - Public



---

## MassRepresentation

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassRepresentation

**Contents:**
- MassRepresentation
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

const UScriptStruct * UE::Mass::Representation::GetTagFromVisibility ( EMassVisibility Visibility )

EMassVisibility UE::Mass::Representation::GetVisibilityFromArchetype ( const FMassExecutionContext& Context )

bool UE::Mass::Representation::IsVisibilityTagSet ( const FMassExecutionContext& Context, EMassVisibility Visibility )



---

## MassSignals

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassSignals

**Contents:**
- MassSignals
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## MassSimulation

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassSimulation

**Contents:**
- MassSimulation
- Navigation
- Classes
- Interfaces



---

## MassSmartObjects

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassSmartObjects

**Contents:**
- MassSmartObjects
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## MassSpawner

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassSpawner

**Contents:**
- MassSpawner
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

bool operator! ( EMassTranslationDirection E )

EMassTranslationDirection operator& ( EMassTranslationDirection Lhs, EMassTranslationDirection Rhs )

EMassTranslationDirection & operator&= ( EMassTranslationDirection& Lhs, EMassTranslationDirection Rhs )

EMassTranslationDirection operator^ ( EMassTranslationDirection Lhs, EMassTranslationDirection Rhs )

EMassTranslationDirection & operator^= ( EMassTranslationDirection& Lhs, EMassTranslationDirection Rhs )

EMassTranslationDirection operator| ( EMassTranslationDirection Lhs, EMassTranslationDirection Rhs )

EMassTranslationDirection & operator|= ( EMassTranslationDirection& Lhs, EMassTranslationDirection Rhs )

EMassTranslationDirection operator~ ( EMassTranslationDirection E )



---

## MassZoneGraphNavigation

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MassZoneGraphNavigation

**Contents:**
- MassZoneGraphNavigation
- Navigation
- Classes
- Structs
- Interfaces



---

## MaterialAnalyzer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MaterialAnalyzer

**Contents:**
- MaterialAnalyzer
- Navigation



---

## MDLImporter

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MDLImporter

**Contents:**
- MDLImporter
- Navigation
- Classes
- Interfaces
- Functions
  - Public

FString UE::Mdl::Util::ConvertFilePathToModuleName ( const TCHAR* FilePath )



---

## MediaCompositingEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MediaCompositingEditor

**Contents:**
- MediaCompositingEditor
- Navigation
- Classes



---

## MediaCompositing

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MediaCompositing

**Contents:**
- MediaCompositing
- Navigation
- Classes
- Structs



---

## MediaFrameworkUtilities

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MediaFrameworkUtilities

**Contents:**
- MediaFrameworkUtilities
- Navigation
- Classes
- Interfaces
- Functions
  - Static

static const FName MediaBundleMaterialParametersName::FailedTextureName ( "FailedTexture" )

static const FName MediaBundleMaterialParametersName::GarbageMatteTextureName ( "GarbageMatteTexture" )

static const FName MediaBundleMaterialParametersName::IsValidMediaName ( "IsValid" )

static const FName MediaBundleMaterialParametersName::LensDisplacementMapTextureName ( "UVDisplacementMapTexture" )

static const FName MediaBundleMaterialParametersName::MediaTextureName ( "MediaTexture" )



---

## MediaIOCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MediaIOCore

**Contents:**
- MediaIOCore
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Functions

bool operator! ( EMediaIOSampleType E )

EMediaIOSampleType operator& ( EMediaIOSampleType Lhs, EMediaIOSampleType Rhs )

EMediaIOSampleType & operator&= ( EMediaIOSampleType& Lhs, EMediaIOSampleType Rhs )

EMediaIOSampleType operator^ ( EMediaIOSampleType Lhs, EMediaIOSampleType Rhs )

EMediaIOSampleType & operator^= ( EMediaIOSampleType& Lhs, EMediaIOSampleType Rhs )

EMediaIOSampleType operator| ( EMediaIOSampleType Lhs, EMediaIOSampleType Rhs )

EMediaIOSampleType & operator|= ( EMediaIOSampleType& Lhs, EMediaIOSampleType Rhs )

EMediaIOSampleType operator~ ( EMediaIOSampleType E )

static FName UE::CaptureCardMediaSource::Deinterlacer ( "Deinterlacer" )

static FName UE::CaptureCardMediaSource::EvaluationType ( "EvaluationType" )

static FName UE::CaptureCardMediaSource::Framelock ( "Framelock" )

static FName UE::CaptureCardMediaSource::InterlaceFieldOrder ( "InterlaceFieldOrder" )

static FName UE::CaptureCardMediaSource::OpenColorIOSettings ( "OpenColorIOSettings" )

static FName UE::CaptureCardMediaSource::OverrideSourceColorSpace ( "OverrideSourceColorSpace" )

static FName UE::CaptureCardMediaSource::OverrideSourceEncoding ( "OverrideSourceEncoding" )

static FName UE::CaptureCardMediaSource::RenderJIT ( "RenderJIT" )

static FName UE::CaptureCardMediaSource::SourceColorSpace ( "SourceColorcSpace" )

static FName UE::CaptureCardMediaSource::SourceEncoding ( "SourceEncoding" )

static EMediaIOTimecodeFormat UE::MediaIO::FromAutoDetectableTimecodeFormat ( EMediaIOAutoDetectableTimecodeFormat TimecodeFormat )

static void UE::MediaIO::LogThrottle ( const FLogCategoryBase& InLogCategory, ELogVerbosity::Type InVerbosity, const FTimespan& InTimeBetweenLogs, const FString& LogDetails, const FString& FileName, int32 LineNumber )

static EMediaIOAutoDetectableTimecodeFormat UE::MediaIO::ToAutoDetectableTimecodeFormat ( EMediaIOTimecodeFormat TimecodeFormat )

static FAutoConsoleCommand UE::MediaIOAudioDebug::CAudioDebug ( TEXT("MediaIO.DumpAudio"), TEXT("[seconds (default: 1)] - Number of seconds to dump audio for."), FConsoleCommandWithArgsDelegate::CreateLambda(const [TArray](API/Runtime/Core/TArray)< [FString](API/Runtime/Core/FString) >&Args { if(Args.Num()) { SecondsToDumpFor..., ECVF_Default )

static FAudioDebugDumpSystem & UE::MediaIOAudioDebug::GetSingleton()

static void UE::MediaIOAudioDebug::Private::SerializeWaveFile ( TArray< uint8 >& OutWaveFileData, const uint8* InPCMData, const int32 NumBytes, const int32 NumChannels, const int32 SampleRate, const int32 BytesPerSample, bool bFloatingPoint )

static void UE::MediaIOAudioDebug::Private::WriteUInt16ToByteArrayLE ( TArray< uint8 >& InByteArray, int32& Index, const uint16 Value )

static void UE::MediaIOAudioDebug::Private::WriteUInt32ToByteArrayLE ( TArray< uint8 >& InByteArray, int32& Index, const uint32 Value )



---

## MediaIOEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MediaIOEditor

**Contents:**
- MediaIOEditor
- Navigation
- Classes
- Structs



---

## MediaMovieStreamer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MediaMovieStreamer

**Contents:**
- MediaMovieStreamer
- Navigation
- Classes



---

## MediaPlateEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MediaPlateEditor

**Contents:**
- MediaPlateEditor
- Navigation
- Classes



---

## MediaPlate

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MediaPlate

**Contents:**
- MediaPlate
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public



---

## MediaPlayerEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MediaPlayerEditor

**Contents:**
- MediaPlayerEditor
- Navigation
- Classes
- Interfaces



---

## MediaStreamEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MediaStreamEditor

**Contents:**
- MediaStreamEditor
- Navigation
- Classes



---

## MediaStream

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MediaStream

**Contents:**
- MediaStream
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Variables
  - Public



---

## MediaViewer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MediaViewer

**Contents:**
- MediaViewer
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Variables
  - Public
- Functions

int32 GetTypeHash ( const FMediaViewerLibraryEntry& InEntry )



---

## MegascansPlugin

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MegascansPlugin

**Contents:**
- MegascansPlugin
- Navigation
- Classes
- Interfaces
- Typedefs



---

## MemoryUsageQueries

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MemoryUsageQueries

**Contents:**
- MemoryUsageQueries
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## MeshFileUtils

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MeshFileUtils

**Contents:**
- MeshFileUtils
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## MeshLODToolset

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MeshLODToolset

**Contents:**
- MeshLODToolset
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## MeshModelingToolsEditorOnlyExp

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MeshModelingToolsEditorOnlyExp

**Contents:**
- MeshModelingToolsEditorOnlyExp
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public



---

## MeshModelingToolsEditorOnly

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MeshModelingToolsEditorOnly

**Contents:**
- MeshModelingToolsEditorOnly
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

bool operator! ( USkeletonEditingTool::EBoneSelectionMode E )

USkeletonEditingTool::EBoneSelectionMode operator& ( USkeletonEditingTool::EBoneSelectionMode Lhs, USkeletonEditingTool::EBoneSelectionMode Rhs )

USkeletonEditingTool::EBoneSelectionMode & operator&= ( USkeletonEditingTool::EBoneSelectionMode& Lhs, USkeletonEditingTool::EBoneSelectionMode Rhs )

USkeletonEditingTool::EBoneSelectionMode operator^ ( USkeletonEditingTool::EBoneSelectionMode Lhs, USkeletonEditingTool::EBoneSelectionMode Rhs )

USkeletonEditingTool::EBoneSelectionMode & operator^= ( USkeletonEditingTool::EBoneSelectionMode& Lhs, USkeletonEditingTool::EBoneSelectionMode Rhs )

USkeletonEditingTool::EBoneSelectionMode operator| ( USkeletonEditingTool::EBoneSelectionMode Lhs, USkeletonEditingTool::EBoneSelectionMode Rhs )

USkeletonEditingTool::EBoneSelectionMode & operator|= ( USkeletonEditingTool::EBoneSelectionMode& Lhs, USkeletonEditingTool::EBoneSelectionMode Rhs )

USkeletonEditingTool::EBoneSelectionMode operator~ ( USkeletonEditingTool::EBoneSelectionMode E )

TArray< FMatrix > SkeletalMeshToolsHelper::ComputeBoneMatrices ( const TArray< FTransform >& ComponentSpaceTransformsRefPose, const TArray< FTransform >& ComponentSpaceTransforms )

void SkeletalMeshToolsHelper::GetPosedMesh ( TFunctionRef< void(int32, const FVector&)> WriteFunc, const FDynamicMesh3& SourceMesh, const TArray< FMatrix >& BoneMatrices, FName SkinWeightProfile, const TMap< FName, float >& MorphTargetWeights )

void SkeletalMeshToolsHelper::GetUnposedMesh ( TFunctionRef< void(FVertInfo, const FVector&)> WriteFunc, const FDynamicMesh3& PosedMesh, const FDynamicMesh3& SourceMesh, const TArray< FMatrix >& BoneMatrices, FName SkinWeightProfile, const TMap< FName, float >& MorphTargetWeights, const TArray< int32 >& VertArray )



---

## MeshModelingToolsExp

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MeshModelingToolsExp

**Contents:**
- MeshModelingToolsExp
- Navigation
- Classes
- Structs
- Enums
  - Public
- Constants
- Functions
  - Public

bool operator! ( EBakeMapType E )

bool operator! ( EBakeOpState E )

EBakeMapType operator& ( EBakeMapType Lhs, EBakeMapType Rhs )

EBakeOpState operator& ( EBakeOpState Lhs, EBakeOpState Rhs )

EBakeMapType & operator&= ( EBakeMapType& Lhs, EBakeMapType Rhs )

EBakeOpState & operator&= ( EBakeOpState& Lhs, EBakeOpState Rhs )

EBakeMapType operator^ ( EBakeMapType Lhs, EBakeMapType Rhs )

EBakeOpState operator^ ( EBakeOpState Lhs, EBakeOpState Rhs )

EBakeMapType & operator^= ( EBakeMapType& Lhs, EBakeMapType Rhs )

EBakeOpState & operator^= ( EBakeOpState& Lhs, EBakeOpState Rhs )

EBakeMapType operator| ( EBakeMapType Lhs, EBakeMapType Rhs )

EBakeOpState operator| ( EBakeOpState Lhs, EBakeOpState Rhs )

EBakeMapType & operator|= ( EBakeMapType& Lhs, EBakeMapType Rhs )

EBakeOpState & operator|= ( EBakeOpState& Lhs, EBakeOpState Rhs )

EBakeMapType operator~ ( EBakeMapType E )

EBakeOpState operator~ ( EBakeOpState E )

void UE::PhysicsTools::InitializeCollisionGeometryVisualization ( UPreviewGeometry* PreviewGeom, UCollisionGeometryVisualizationProperties* Settings, const FPhysicsDataCollection& PhysicsData, float DepthBias, int32 CircleStepResolution, bool bClearExistingLinesAndTriangles )

void UE::PhysicsTools::InitializePhysicsToolObjectPropertySet ( const FPhysicsDataCollection* PhysicsData, UPhysicsObjectToolPropertySet* PropSet )

void UE::PhysicsTools::PartiallyInitializeCollisionGeometryVisualization ( UPreviewGeometry* PartialPreviewGeom, UCollisionGeometryVisualizationProperties* Settings, const FPhysicsDataCollection& PhysicsData, int32 ColorIndex, float DepthBias, int32 CircleStepResolution )

void UE::PhysicsTools::PartiallyUpdateCollisionGeometryVisualization ( UPreviewGeometry* PartialPreviewGeom, UCollisionGeometryVisualizationProperties* Settings, int32 ColorIndex )

void UE::PhysicsTools::UpdateCollisionGeometryVisualization ( UPreviewGeometry* PreviewGeom, UCollisionGeometryVisualizationProperties* Settings )



---

## MeshModelingTools

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MeshModelingTools

**Contents:**
- MeshModelingTools
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Variables
  - Public
- Functions

UPolyEditPreviewMesh * UE::Geometry::PolyEditActivityUtil::CreatePolyEditPreviewMesh ( UInteractiveTool& Tool, const UPolyEditActivityContext& ActivityContext )

void UE::Geometry::PolyEditActivityUtil::UpdatePolyEditPreviewMaterials ( UInteractiveTool& Tool, const UPolyEditActivityContext& ActivityContext, UPolyEditPreviewMesh& EditPreviewMesh, EPreviewMaterialType MaterialType )

void UE::SculptUtil::PrecalculateNormalsROI ( const FDynamicMesh3* Mesh, const TArray< int32 >& TriangleROI, FUniqueIndexSet& IndexSetTemp, bool& bIsOverlayElementsOut, bool bForceVertex )

void UE::SculptUtil::PrecalculateNormalsROI ( const FDynamicMesh3* Mesh, const TArray< int32 >& TriangleROI, TArray< std::atomic< bool > >& ROIFlags, bool& bIsOverlayElementsOut, bool bForceVertex )

void UE::SculptUtil::RecalculateNormals_Overlay ( FDynamicMesh3* Mesh, const TSet< int32 >& ModifiedTris, FUniqueIndexSet& ElementSetTemp )

void UE::SculptUtil::RecalculateNormals_Overlay ( FDynamicMesh3* Mesh, const TSet< int32 >& ModifiedTris, TSet< int32 >& ElementSetBuffer, TArray< int32 >& NormalsBuffer )

void UE::SculptUtil::RecalculateNormals_PerVertex ( FDynamicMesh3* Mesh, const TSet< int32 >& ModifiedTris, FUniqueIndexSet& VertexSetTemp )

void UE::SculptUtil::RecalculateNormals_PerVertex ( FDynamicMesh3* Mesh, const TSet< int32 >& ModifiedTris, TSet< int32 >& VertexSetBuffer, TArray< int32 >& NormalsBuffer )

void UE::SculptUtil::RecalculateROINormalForTriangles ( FDynamicMesh3* Mesh, TArray< int > Triangles, bool bIsOverlayElements )

void UE::SculptUtil::RecalculateROINormals ( FDynamicMesh3* Mesh, const TArray< int32 >& Indices, bool bIsOverlayElements )

void UE::SculptUtil::RecalculateROINormals ( FDynamicMesh3* Mesh, TArray< std::atomic< bool > >& ROIFlags, bool bIsOverlayElements )

void UE::SculptUtil::RecalculateROINormals ( FDynamicMesh3* Mesh, const TSet< int32 >& TriangleROI, FUniqueIndexSet& IndexSetTemp, bool bForceVertex )

void UE::SculptUtil::RecalculateROINormals ( FDynamicMesh3* Mesh, const TSet< int32 >& TriangleROI, TSet< int32 >& TempSetBuffer, TArray< int32 >& NormalsBuffer, bool bForceVertex )

static ELaplacianWeightScheme ConvertToLaplacianWeightScheme ( const EWeightScheme WeightScheme )

static TUniqueFunction< double(const FSculptBrushStamp &, const FVector3d &)> UE::SculptFalloffs::MakeInverseBoxFalloff()

static TUniqueFunction< double(const FSculptBrushStamp &, const FVector3d &)> UE::SculptFalloffs::MakeInverseFalloff()

static TUniqueFunction< double(const FSculptBrushStamp &, const FVector3d &)> UE::SculptFalloffs::MakeLinearBoxFalloff()

static TUniqueFunction< double(const FSculptBrushStamp &, const FVector3d &)> UE::SculptFalloffs::MakeLinearFalloff()

static TUniqueFunction< double(const FSculptBrushStamp &, const FVector3d &)> UE::SculptFalloffs::MakeRoundBoxFalloff()

static TUniqueFunction< double(const FSculptBrushStamp &, const FVector3d &)> UE::SculptFalloffs::MakeRoundFalloff()

static TUniqueFunction< double(const FSculptBrushStamp &, const FVector3d &)> UE::SculptFalloffs::MakeSmoothBoxFalloff()

static TUniqueFunction< double(const FSculptBrushStamp &, const FVector3d &)> UE::SculptFalloffs::MakeStandardSmoothFalloff()



---

## MeshPaintEditorMode

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MeshPaintEditorMode

**Contents:**
- MeshPaintEditorMode
- Navigation
- Classes
- Enums
  - Public



---

## MeshPaintingToolset

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MeshPaintingToolset

**Contents:**
- MeshPaintingToolset
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants



---

## MeshResizingCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MeshResizingCore

**Contents:**
- MeshResizingCore
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## MeshResizingDataflowNodes

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MeshResizingDataflowNodes

**Contents:**
- MeshResizingDataflowNodes
- Navigation
- Structs



---

## MeshTrackerInterface

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MeshTrackerInterface

**Contents:**
- MeshTrackerInterface
- Navigation
- Interfaces



---

## MetaHumanBatchProcessor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanBatchProcessor

**Contents:**
- MetaHumanBatchProcessor
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

bool operator! ( EBatchOperationStepsFlags E )

EBatchOperationStepsFlags operator& ( EBatchOperationStepsFlags Lhs, EBatchOperationStepsFlags Rhs )

EBatchOperationStepsFlags & operator&= ( EBatchOperationStepsFlags& Lhs, EBatchOperationStepsFlags Rhs )

EBatchOperationStepsFlags operator^ ( EBatchOperationStepsFlags Lhs, EBatchOperationStepsFlags Rhs )

EBatchOperationStepsFlags & operator^= ( EBatchOperationStepsFlags& Lhs, EBatchOperationStepsFlags Rhs )

EBatchOperationStepsFlags operator| ( EBatchOperationStepsFlags Lhs, EBatchOperationStepsFlags Rhs )

EBatchOperationStepsFlags & operator|= ( EBatchOperationStepsFlags& Lhs, EBatchOperationStepsFlags Rhs )

EBatchOperationStepsFlags operator~ ( EBatchOperationStepsFlags E )



---

## MetaHumanCalibrationCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanCalibrationCore

**Contents:**
- MetaHumanCalibrationCore
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

TArray< int32 > UE::MetaHuman::Image::FilterFrameIndices ( const TPair< TArray< FString >, TArray< FString > >& InImagePaths, Predicate&& InPredicate )

TPair< TArray< FString >, TArray< FString > > UE::MetaHuman::Image::FilterFramePaths ( const UFootageCaptureData* InCaptureData, Predicate&& InPredicate )

TPair< TArray< FString >, TArray< FString > > UE::MetaHuman::Image::FilterFramePaths ( const TPair< TArray< FString >, TArray< FString > >& InImagePaths, Predicate&& InPredicate )



---

## MetaHumanCalibrationLib

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanCalibrationLib

**Contents:**
- MetaHumanCalibrationLib
- Navigation
- Classes



---

## MetaHumanCaptureDataEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanCaptureDataEditor

**Contents:**
- MetaHumanCaptureDataEditor
- Navigation
- Classes



---

## MetaHumanCaptureData

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanCaptureData

**Contents:**
- MetaHumanCaptureData
- Navigation
- Classes
- Structs



---

## MetaHumanCaptureProtocolStack

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanCaptureProtocolStack

**Contents:**
- MetaHumanCaptureProtocolStack
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Functions
  - Public

class UE_DEPRECATED (

class UE_DEPRECATED (

class UE_DEPRECATED (

class UE_DEPRECATED (



---

## MetaHumanCaptureSource

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanCaptureSource

**Contents:**
- MetaHumanCaptureSource
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Variables
  - Public
- Functions

FConnectionChangedEvent ( EState InConnectionState )

FRecordingStatusChangedEvent ( bool bInIsRecording )

FTakesRemovedEvent ( TArray< TakeId > InTakesRemoved )

FTakesRemovedEvent ( TakeId InTakeRemoved )

FThumbnailChangedEvent ( TakeId InChangedTake )



---

## MetaHumanCaptureUtils

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanCaptureUtils

**Contents:**
- MetaHumanCaptureUtils
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

virtual TArray< FString > detail::GetAvailableEvents()

TScopeGuard< Fun > detail::operator+ ( FScopeGuardOnExit, Fun&& InFn )

virtual void detail::SubscribeToEvent ( const FString& InEventName, FCaptureEventHandler InHandler )

virtual void detail::UnsubscribeAll()

TScopeGuard< FuncType > MakeScopeGuard ( FuncType InFunc )

void detail::PublishEventInternal ( TSharedPtr< const FCaptureEvent > InEvent ) const

void detail::RegisterEvent ( const FString& InEventName )

static void details::ExecuteDelegate ( TDelegate< void(Args...)> InDelegate, EDelegateExecutionThread InThread, Args&&... InArgs )



---

## MetaHumanCharacterEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanCharacterEditor

**Contents:**
- MetaHumanCharacterEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

ENUM_RANGE_BY_COUNT ( EMetaHumanCharacterAccentRegion, EMetaHumanCharacterAccentRegion::Count )

ENUM_RANGE_BY_COUNT ( EMetaHumanCharacterAccentRegionParameter, EMetaHumanCharacterAccentRegionParameter::Count )

ENUM_RANGE_BY_COUNT ( EMetaHumanCharacterFrecklesParameter, EMetaHumanCharacterFrecklesParameter::Count )



---

## MetaHumanCharacterPaletteEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanCharacterPaletteEditor

**Contents:**
- MetaHumanCharacterPaletteEditor
- Navigation
- Classes
- Interfaces
- Enums
  - Public



---

## MetaHumanCharacterPalette

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanCharacterPalette

**Contents:**
- MetaHumanCharacterPalette
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## MetaHumanCharacter

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanCharacter

**Contents:**
- MetaHumanCharacter
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

UE::MetaHuman::GeometryRemoval::USTRUCT ( BlueprintType )



---

## MetaHumanConfigEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanConfigEditor

**Contents:**
- MetaHumanConfigEditor
- Navigation
- Classes



---

## MetaHumanConfig

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanConfig

**Contents:**
- MetaHumanConfig
- Navigation
- Classes
- Enums
  - Public



---

## MetaHumanCoreEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanCoreEditor

**Contents:**
- MetaHumanCoreEditor
- Navigation
- Classes
- Interfaces
- Typedefs



---

## MetaHumanCoreTechLib

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanCoreTechLib

**Contents:**
- MetaHumanCoreTechLib
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## MetaHumanCoreTech

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanCoreTech

**Contents:**
- MetaHumanCoreTech
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## MetaHumanCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanCore

**Contents:**
- MetaHumanCore
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Functions
  - Public

UCameraCalibration * LoadLiveLinkFaceCameraCalibration ( UClass* InClass, UObject* InParent, FName InName, EObjectFlags InFlags, const FString& InFilenameOrString, bool bIsFile )

bool operator! ( EDNARigCompatiblityFlags E )

EDNARigCompatiblityFlags operator& ( EDNARigCompatiblityFlags Lhs, EDNARigCompatiblityFlags Rhs )

EDNARigCompatiblityFlags & operator&= ( EDNARigCompatiblityFlags& Lhs, EDNARigCompatiblityFlags Rhs )

EDNARigCompatiblityFlags operator^ ( EDNARigCompatiblityFlags Lhs, EDNARigCompatiblityFlags Rhs )

EDNARigCompatiblityFlags & operator^= ( EDNARigCompatiblityFlags& Lhs, EDNARigCompatiblityFlags Rhs )

EDNARigCompatiblityFlags operator| ( EDNARigCompatiblityFlags Lhs, EDNARigCompatiblityFlags Rhs )

EDNARigCompatiblityFlags & operator|= ( EDNARigCompatiblityFlags& Lhs, EDNARigCompatiblityFlags Rhs )

EDNARigCompatiblityFlags operator~ ( EDNARigCompatiblityFlags E )



---

## MetaHumanDefaultEditorPipeline

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanDefaultEditorPipeline

**Contents:**
- MetaHumanDefaultEditorPipeline
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## MetaHumanDefaultPipeline

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanDefaultPipeline

**Contents:**
- MetaHumanDefaultPipeline
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

void UE::MetaHuman::MaterialUtils::SetInstanceParameters ( const TArray< FMetaHumanMaterialParameter >& InMaterialParameters, const TMap< FName, TObjectPtr< UMaterialInstanceDynamic > >& InMaterialInstanceMapping, const TArray< FName >& InAvailableSlots, const FInstancedPropertyBag& InPropertyBag )



---

## MetaHumanFaceAnimationSolver

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanFaceAnimationSolver

**Contents:**
- MetaHumanFaceAnimationSolver
- Navigation
- Classes
- Enums
  - Public



---

## MetaHumanFaceContourTracker

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanFaceContourTracker

**Contents:**
- MetaHumanFaceContourTracker
- Navigation
- Classes



---

## MetaHumanFaceFittingSolver

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanFaceFittingSolver

**Contents:**
- MetaHumanFaceFittingSolver
- Navigation
- Classes



---

## MetaHumanFootageIngest

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanFootageIngest

**Contents:**
- MetaHumanFootageIngest
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## MetaHumanIdentity

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanIdentity

**Contents:**
- MetaHumanIdentity
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public



---

## MetaHumanImageViewerEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanImageViewerEditor

**Contents:**
- MetaHumanImageViewerEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## MetaHumanImageViewer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanImageViewer

**Contents:**
- MetaHumanImageViewer
- Navigation
- Classes
- Typedefs



---

## MetaHumanLiveLinkSourceEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanLiveLinkSourceEditor

**Contents:**
- MetaHumanLiveLinkSourceEditor
- Navigation
- Classes



---

## MetaHumanLiveLinkSource

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanLiveLinkSource

**Contents:**
- MetaHumanLiveLinkSource
- Navigation
- Classes
- Enums
  - Public
- Functions
  - Public

bool operator! ( EMetaHumanLiveLinkHeadPoseMode E )

EMetaHumanLiveLinkHeadPoseMode operator& ( EMetaHumanLiveLinkHeadPoseMode Lhs, EMetaHumanLiveLinkHeadPoseMode Rhs )

EMetaHumanLiveLinkHeadPoseMode & operator&= ( EMetaHumanLiveLinkHeadPoseMode& Lhs, EMetaHumanLiveLinkHeadPoseMode Rhs )

EMetaHumanLiveLinkHeadPoseMode operator^ ( EMetaHumanLiveLinkHeadPoseMode Lhs, EMetaHumanLiveLinkHeadPoseMode Rhs )

EMetaHumanLiveLinkHeadPoseMode & operator^= ( EMetaHumanLiveLinkHeadPoseMode& Lhs, EMetaHumanLiveLinkHeadPoseMode Rhs )

EMetaHumanLiveLinkHeadPoseMode operator| ( EMetaHumanLiveLinkHeadPoseMode Lhs, EMetaHumanLiveLinkHeadPoseMode Rhs )

EMetaHumanLiveLinkHeadPoseMode & operator|= ( EMetaHumanLiveLinkHeadPoseMode& Lhs, EMetaHumanLiveLinkHeadPoseMode Rhs )

EMetaHumanLiveLinkHeadPoseMode operator~ ( EMetaHumanLiveLinkHeadPoseMode E )



---

## MetaHumanLocalLiveLinkSource

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanLocalLiveLinkSource

**Contents:**
- MetaHumanLocalLiveLinkSource
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## MetaHumanPerformance

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanPerformance

**Contents:**
- MetaHumanPerformance
- Navigation
- Classes
- Enums
  - Public



---

## MetaHumanPipelineCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanPipelineCore

**Contents:**
- MetaHumanPipelineCore
- Navigation
- Classes
- Typedefs
- Enums
  - Public



---

## MetaHumanPipeline

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanPipeline

**Contents:**
- MetaHumanPipeline
- Navigation
- Classes
- Functions
  - Public

bool DoesNNEAssetExist ( const FString& InAssetPath )



---

## MetaHumanPlatform

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanPlatform

**Contents:**
- MetaHumanPlatform
- Navigation
- Classes



---

## MetaHumanSDKEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanSDKEditor

**Contents:**
- MetaHumanSDKEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## MetaHumanSDKRuntime

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanSDKRuntime

**Contents:**
- MetaHumanSDKRuntime
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public
  - Static

void MetaHumanComponentHelpers::ConnectVariable ( UAnimInstance* AnimInstance, const FName& InIdentifier, const PropertyVarType& InVar )

static bool MetaHumanComponentHelpers::GetPropertyValue ( UObject* InObject, FStringView InPropertyName, T& OutPropertyValue )



---

## MetaHumanSequencer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanSequencer

**Contents:**
- MetaHumanSequencer
- Navigation
- Classes
- Structs



---

## MetaHumanSpeech2Face

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanSpeech2Face

**Contents:**
- MetaHumanSpeech2Face
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## MetaHumanToolkit

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetaHumanToolkit

**Contents:**
- MetaHumanToolkit
- Navigation
- Classes
- Structs
- Typedefs



---

## MetasoundEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetasoundEditor

**Contents:**
- MetasoundEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## MetasoundEngineTest

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetasoundEngineTest

**Contents:**
- MetasoundEngineTest
- Navigation
- Classes



---

## MetasoundEngine

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetasoundEngine

**Contents:**
- MetasoundEngine
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

const FNodeClassName & Metasound::AudioBusWriterNode::GetClassName()

Metasound::AudioBusWriterNode::Inputs::DECLARE_METASOUND_PARAM ( METASOUNDENGINE_API, AudioBus )

Metasound::AudioBusWriterNode::Inputs::DECLARE_METASOUND_PARAM ( METASOUNDENGINE_API, Audio )

Metasound::DECLARE_METASOUND_DATA_REFERENCE_TYPES ( FAudioBusAsset, FAudioBusAssetTypeInfo, FAudioBusAssetReadRef, FAudioBusAssetWriteRef )

Metasound::DECLARE_METASOUND_DATA_REFERENCE_TYPES ( WaveTable::FWaveTable, METASOUNDENGINE_API, FWaveTableTypeInfo, FWaveTableReadRef, FWaveTableWriteRef )

Metasound::DECLARE_METASOUND_DATA_REFERENCE_TYPES ( FEnumWaveTableEnvelopeMode, METASOUNDENGINE_API, FEnumWaveTableEnvelopeModeTypeInfo, FEnumWaveTableEnvelopeModeReadRef, FEnumWaveTableEnvelopeModeWriteRef )

Metasound::DECLARE_METASOUND_DATA_REFERENCE_TYPES ( FEnumWaveTableInterpolationMode, METASOUNDENGINE_API, FEnumWaveTableInterpModeTypeInfo, FEnumWaveTableInterpModeReadRef, FEnumWaveTableInterpModeWriteRef )



---

## MetasoundExperimentalEngineRuntime

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetasoundExperimentalEngineRunti-

**Contents:**
- MetasoundExperimentalEngineRuntime
- Navigation
- Classes
- Structs



---

## MetasoundExperimentalRuntime

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetasoundExperimentalRuntime

**Contents:**
- MetasoundExperimentalRuntime
- Navigation
- Classes
- Structs
- Typedefs



---

## MetasoundFrontend

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetasoundFrontend

**Contents:**
- MetasoundFrontend
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

FString LexToString ( const EMetasoundFrontendClassAccessFlags& InFlag )

const TCHAR * LexToString ( EMetasoundFrontendClassType InClassType )

const TCHAR * LexToString ( EMetasoundFrontendVertexAccessType InVertexAccess )

virtual Metasound::~TExecutableLiteralOperator()

virtual Metasound::~TLiteralOperator()

virtual void Metasound::BindInputs ( FInputVertexInterfaceData& InVertexData )

virtual void Metasound::BindOutputs ( FOutputVertexInterfaceData& InVertexData )

const DerivedAddressType * Metasound::CastAddressType ( const FTransmissionAddress& InOther )

TSenderPtr< TDataType > Metasound::Downcast ( TUniquePtr< ISender >&& InPtr )

TReceiverPtr< TDataType > Metasound::Downcast ( TUniquePtr< IReceiver >&& InPtr )

void Metasound::Execute()

ToAccessPtrType Metasound::Frontend::ConstCastAccessPtr ( const FromAccessPtrType& InAccessPtr )

FGuid Metasound::Frontend::DefaultPageID ( 0, 0, 0, 0 )

const ElementType * Metasound::Frontend::FindPreferredPage ( const TArray< ElementType >& InElements, TArrayView< const FGuid > InPageOrder )

FMetasoundFrontendClass Metasound::Frontend::GenerateClass ()

FMetasoundFrontendClass Metasound::Frontend::GenerateClass ( const FNodeInitData& InNodeInitData )

AccessPtrType Metasound::Frontend::MakeAccessPtr ( const FAccessPoint& InAccessPoint, Type& InRef )

void Metasound::Frontend::MetasoundDataTypeRegistrationPrivate::AttemptToRegisterConverter ( const FModuleInfo& InModuleInfo )

void Metasound::Frontend::MetasoundDataTypeRegistrationPrivate::AttemptToRegisterSendAndReceiveNodes ( const FModuleInfo& InModuleInfo )

Frontend::FDataTypeRegistryInfo Metasound::Frontend::MetasoundDataTypeRegistrationPrivate::CreateDataTypeInfo()

TSharedPtr< Frontend::IEnumDataTypeInterface > Metasound::Frontend::MetasoundDataTypeRegistrationPrivate::GetEnumDataTypeInterface ()

void Metasound::Frontend::MetasoundDataTypeRegistrationPrivate::RegisterConverterNodes ( const FModuleInfo& InModuleInfo )

bool Metasound::Frontend::MetasoundDataTypeRegistrationPrivate::RegisterDataTypeArrayWithFrontend ( const FModuleInfo& InModuleInfo )

bool Metasound::Frontend::MetasoundDataTypeRegistrationPrivate::RegisterDataTypeWithFrontendInternal ( const FModuleInfo& InModuleInfo )

void Metasound::Frontend::NodeRegistrationPrivate::TriggerDeprecatedNodeConstructorWarning()

void Metasound::Frontend::NodeRegistrationPrivate::TriggerMissingCreateNodeClassMetadataWarning()

bool Metasound::Frontend::RegisterArrayNodes ( const FModuleInfo& InModuleInfo )

bool Metasound::Frontend::RegisterDataType ()

bool Metasound::Frontend::RegisterDataType ( const FModuleInfo& InModuleInfo )

bool Metasound::Frontend::RegisterNode ()

bool Metasound::Frontend::RegisterNode ( const FNodeClassMetadata& InMetadata )

bool Metasound::Frontend::RegisterNode ( const FModuleInfo& InOwningModuleInfo )

bool Metasound::Frontend::RegisterNode ( const FNodeClassMetadata& InMetadata, const FModuleInfo& InOwningModuleInfo )

bool Metasound::Frontend::UnregisterNode ()

bool Metasound::Frontend::UnregisterNode ( const FModuleInfo& InOwningModuleInfo )

virtual FDataReferenceCollection Metasound::GetInputs()

virtual FDataReferenceCollection Metasound::GetOutputs()

uint32 Metasound::GetTypeHash ( const Metasound::FTransmissionAddress& )

TSharedRef< IDataChannel, ESPMode::ThreadSafe > Metasound::MakeDataChannel ( const FOperatorSettings& InSettings )

bool Metasound::MetasoundArrayNodesPrivate::RegisterArrayConcatNode ( const Frontend::FModuleInfo& InModuleInfo )

bool Metasound::MetasoundArrayNodesPrivate::RegisterArrayGetNode ( const Frontend::FModuleInfo& InModuleInfo )

bool Metasound::MetasoundArrayNodesPrivate::RegisterArrayLastIndexNode ( const Frontend::FModuleInfo& InModuleInfo )

bool Metasound::MetasoundArrayNodesPrivate::RegisterArrayNumNode ( const Frontend::FModuleInfo& InModuleInfo )

bool Metasound::MetasoundArrayNodesPrivate::RegisterArrayRandomGetNode ( const Frontend::FModuleInfo& InModuleInfo )

bool Metasound::MetasoundArrayNodesPrivate::RegisterArraySetNode ( const Frontend::FModuleInfo& InModuleInfo )

bool Metasound::MetasoundArrayNodesPrivate::RegisterArrayShuffleNode ( const Frontend::FModuleInfo& InModuleInfo )

bool Metasound::MetasoundArrayNodesPrivate::RegisterArraySubsetNode ( const Frontend::FModuleInfo& InModuleInfo )

bool Metasound::RegisterArrayNodes()

bool Metasound::RegisterDataTypeWithFrontend()

bool Metasound::RegisterNodeWithFrontend ()

bool Metasound::RegisterNodeWithFrontend ( const Metasound::FNodeClassMetadata& InMetadata )

void Metasound::Reset ( const IOperator::FResetParams& InParams )

Metasound::TExecutableLiteralOperator ( const FOperatorSettings& InSettings, const FLiteral& InLiteral )

Metasound::TLiteralOperator ( TDataValueReference< DataType > InValue )

FGuid MetasoundArrayHashPrivate::GetArrayContentHashGuid ( const TArray< ElementType >& InArray )

bool operator! ( EMetasoundFrontendClassAccessFlags E )

EMetasoundFrontendClassAccessFlags operator& ( EMetasoundFrontendClassAccessFlags Lhs, EMetasoundFrontendClassAccessFlags Rhs )

EMetasoundFrontendClassAccessFlags & operator&= ( EMetasoundFrontendClassAccessFlags& Lhs, EMetasoundFrontendClassAccessFlags Rhs )

EMetasoundFrontendClassAccessFlags operator^ ( EMetasoundFrontendClassAccessFlags Lhs, EMetasoundFrontendClassAccessFlags Rhs )

EMetasoundFrontendClassAccessFlags & operator^= ( EMetasoundFrontendClassAccessFlags& Lhs, EMetasoundFrontendClassAccessFlags Rhs )

EMetasoundFrontendClassAccessFlags operator| ( EMetasoundFrontendClassAccessFlags Lhs, EMetasoundFrontendClassAccessFlags Rhs )

EMetasoundFrontendClassAccessFlags & operator|= ( EMetasoundFrontendClassAccessFlags& Lhs, EMetasoundFrontendClassAccessFlags Rhs )

EMetasoundFrontendClassAccessFlags operator~ ( EMetasoundFrontendClassAccessFlags E )

bool RegisterConversionNode ( const Metasound::FVertexName& FromPin, const Metasound::FVertexName& ToPin, const Metasound::FNodeClassMetadata& InNodeMetadata )

static uint8 Metasound::TestForConstructor ( ... )



---

## MetasoundGenerator

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetasoundGenerator

**Contents:**
- MetasoundGenerator
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## MetasoundGraphCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetasoundGraphCore

**Contents:**
- MetasoundGraphCore
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

FString LexToString ( Metasound::EDataReferenceAccessType InAccessType )

FString LexToString ( const Metasound::FLiteral& InLiteral )

FString LexToString ( Metasound::EVertexAccessType InAccessType )

void Metasound::AddBuildError ( FBuildErrorArray& OutErrors, ArgTypes&&... Args )

TMetasoundEnvironmentVariable< Type > & Metasound::CastMetasoundEnvironmentVariableChecked ( IMetasoundEnvironmentVariable& InVar )

const TMetasoundEnvironmentVariable< Type > & Metasound::CastMetasoundEnvironmentVariableChecked ( const IMetasoundEnvironmentVariable& InVar )

std::enable_if_t< std::conjunction_v< std::is_base_of< TOperatorData< std::decay_t< DesiredOperatorDataType > >, DesiredOperatorDataType >, std::is_base_of< IOperatorData, ProvidedOperatorDataType > >, DesiredOperatorDataType * > Metasound::CastOperatorData ( ProvidedOperatorDataType* InOperatorData )

FDataReferenceID Metasound::GetDataReferenceID ( const IDataReference& InDataReference )

const FText & Metasound::GetMetasoundDataTypeDisplayText()

const void *const Metasound::GetMetasoundDataTypeId ()

const FName & Metasound::GetMetasoundDataTypeName()

const FString & Metasound::GetMetasoundDataTypeString()

FMetasoundEnvironmentVariableTypeId Metasound::GetMetasoundEnvironmentVariableTypeId()

FName Metasound::GetStaticOperatorDataTypeName()

bool Metasound::IsChildOf ( const FName InBaseType )

bool Metasound::IsDataReferenceOfType ( const IDataReference& InReference )

bool Metasound::IsDataReferenceOfType ( const IDataReference& InReference )

bool Metasound::IsEnvironmentVariableOfType ( const IMetasoundEnvironmentVariable& InVar )

bool Metasound::IsOperatorDataOfType ( const IOperatorData& InNodeConfig )

FNodeDataVertexKey Metasound::MakeDestinationDataVertexKey ( const FInputDataDestination& InDestination )

TSharedRef< FactoryType, ESPMode::ThreadSafe > Metasound::MakeOperatorFactoryRef ( ArgTypes&&... Args )

FNodeDataVertexKey Metasound::MakeSourceDataVertexKey ( const FOutputDataSource& InSource )

TSharedRef< Base, ESPMode::NotThreadSafe > Metasound::MetasoundDataReferencePrivate::MakeRefOf ( ArgTypes&&... args )

ELiteralType Metasound::MetasoundLiteralIntrinsics::GetLiteralArgTypeFromDecayed ()

ELiteralType Metasound::MetasoundLiteralIntrinsics::GetLiteralArgTypeFromDecayed ()

TDataValueReference< T > Metasound::ValueCast ( const TDataReadReference< T >& InRef )

TDataValueReference< T > Metasound::ValueCast ( const TDataWriteReference< T >& InRef )

const FNodeClassName & Metasound::VariableNames::GetVariableAccessorNodeClassName()

const FNodeClassName & Metasound::VariableNames::GetVariableDeferredAccessorNodeClassName()

const FNodeClassName & Metasound::VariableNames::GetVariableMutatorNodeClassName()

const FNodeClassName & Metasound::VariableNames::GetVariableNodeClassName()

TDataWriteReference< DataType > Metasound::WriteCast ( const TDataReadReference< DataType >& InReadableRef )



---

## MetasoundStandardNodes

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MetasoundStandardNodes

**Contents:**
- MetasoundStandardNodes
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Constants
- Functions
  - Public

Generates a random float value when triggered. | MetasoundRandomNode.h |

Compares two inputs against enumerated comparison types. | MetasoundTriggerCompareNode.h |

Generates a random float value when triggered. | MetasoundValueNode.h |

Metasound::FGain ( float InValue )

PRAGMA_DISABLE_DEPRECATION_WARNINGS Metasound::FGain ( float InValue, EGainRepresentation InRep )

float Metasound::GetDecibels()

float Metasound::GetLinear()

Metasound::operator float()

FGain & Metasound::operator*= ( const FGain& InOther )

FGain & Metasound::operator/= ( const FGain& InOther )

FGain & Metasound::operator+= ( const FGain& InOther )

FGain & Metasound::operator-= ( const FGain& InOther )

void Metasound::SetDecibels ( float InDecibels )

void Metasound::SetLinear ( float InLinearScale )



---

## MicrosoftSpatialSound

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MicrosoftSpatialSound

**Contents:**
- MicrosoftSpatialSound
- Navigation
- Classes
- Structs



---

## MIDIDevice

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MIDIDevice

**Contents:**
- MIDIDevice
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public



---

## MixedRealityCaptureFramework

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MixedRealityCaptureFramework

**Contents:**
- MixedRealityCaptureFramework
- Navigation
- Classes
- Structs
- Interfaces



---

## MLAdapterTestSuite

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MLAdapterTestSuite

**Contents:**
- MLAdapterTestSuite
- Navigation
- Interfaces



---

## MLAdapter

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MLAdapter

**Contents:**
- MLAdapter
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Functions

RetType CallOnGameThread ( TFunction< RetType()> InFunction )

void CallOnGameThread ( TFunction< void()> InFunction )

FString EnumToString ( const EMLAdapterSpaceType Value )

bool FMLAdapter::JsonStringToStruct ( const FString& JsonString, StructType& OutStruct )

T * FMLAdapter::NewObject ( UObject* Outer )

T * FMLAdapter::NewObject ( UObject* Outer, UClass* Class, FName Name, EObjectFlags Flags, UObject* Template, bool bCopyTransientsFromClassDefaults, FObjectInstancingGraph* InInstanceGraph )

FString FMLAdapter::StructArrayToJsonString ( const TArray< StructType >& InStructArray )

FString FMLAdapter::StructToJsonString ( const StructType& InStruct )

TArray< T > FMLAdapter::VectorToArray ( const std::vector< T > InVector )



---

## MLDeformerFrameworkEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MLDeformerFrameworkEditor

**Contents:**
- MLDeformerFrameworkEditor
- Navigation
- Classes
- Typedefs
- Enums
  - Public
- Variables
  - Public
- Functions
  - Public

ETrainingResult UE::MLDeformer::TrainModel ( FMLDeformerEditorModel* EditorModel )

static T * UE::MLDeformer::NewDerivedObject ()



---

## MLDeformerFramework

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MLDeformerFramework

**Contents:**
- MLDeformerFramework
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Constants
- Variables
  - Public

virtual ~UMLDeformerModel()

virtual void BeginDestroy()

virtual UMLDeformerInputInfo * CreateInputInfo()

virtual UMLDeformerModelInstance * CreateModelInstance ( UMLDeformerComponent* Component )

virtual bool DoesSupportBones ()

virtual bool DoesSupportCurves ()

virtual bool DoesSupportLOD ()

virtual bool DoesSupportQualityLevels ()

const FTransform & GetAlignmentTransform ()

const UAnimSequence * GetAnimSequence ()

virtual void GetAssetRegistryTags ( FAssetRegistryTagsContext Context ) const

virtual void GetAssetRegistryTags ( TArray< FAssetRegistryTag >& OutTags ) const

TArray< FBoneReference > & GetBoneIncludeList ()

uint64 GetCookedAssetSizeInBytes ()

TArray< FMLDeformerCurveReference > & GetCurveIncludeList ()

virtual FString GetDefaultDeformerGraphAssetPath ()

UMLDeformerAsset * GetDeformerAsset()

float GetDeltaCutoffLength ()

virtual FString GetDisplayName ()

uint64 GetEditorAssetSizeInBytes ()

uint64 GetGPUMemUsageInBytes()

UMLDeformerInputInfo * GetInputInfo ()

uint64 GetMainMemUsageInBytes()

const int32 GetMaxNumLODs ()

uint64 GetMemUsageInBytes ( UE::MLDeformer::EMemUsageRequestFlags Flags ) const

FNeuralNetworkModifyDelegate & GetNeuralNetworkModifyDelegate()

int32 GetNumBaseMeshVerts ()

virtual int32 GetNumFloatsPerBone()

virtual int32 GetNumFloatsPerCurve()

int32 GetNumTargetMeshVerts ()

bool GetRecoverStrippedDataAfterCook ()

FMLDeformerReinitModelInstancesDelegate & GetReinitModelInstanceDelegate ()

const USkeletalMesh * GetSkeletalMesh ()

virtual USkeleton * GetSkeleton ( bool& bInvalidSkeletonIsError, const IPropertyHandle* PropertyHandle )

UMLDeformerTrainingDataProcessorSettings * GetTrainingDataProcessorSettings ()

const FString & GetTrainingDevice()

const TArray< FString > & GetTrainingDeviceList()

int32 GetTrainingFrameLimit ()

TArray< FName > GetVertexAttributeNames ()

const TArray< int32 > & GetVertexMap ()

const UE::MLDeformer::FVertexMapBuffer & GetVertexMapBuffer ()

UMLDeformerVizSettings * GetVizSettings ()

virtual bool HasTrainingGroundTruth ()

virtual void Init ( UMLDeformerAsset* InDeformerAsset )

virtual void InitGPUData ()

void InitVertexMap ()

void InvalidateMemUsage()

virtual bool IsCompatibleDebugActor ( const AActor* Actor, UMLDeformerComponent** OutDebugComponent ) const

bool IsMemUsageInvalidated()

virtual bool IsNeuralNetworkOnGPU ()

virtual bool IsReadyForFinishDestroy()

virtual bool IsTrained()

FMLDeformerModelOnPostEditProperty & OnPostEditChangeProperty()

FMLDeformerModelOnPostEditUndo & OnPostEditUndo()

FMLDeformerModelOnPostTransacted & OnPostTransacted()

FMLDeformerModelOnPreEditUndo & OnPreEditUndo()

virtual void PostEditChangeProperty ( FPropertyChangedEvent& PropertyChangedEvent )

virtual void PostEditUndo()

virtual void PostLoad()

virtual void PostTransacted ( const FTransactionObjectEvent& Event )

virtual void PreEditUndo()

virtual void PreSave ( FObjectPreSaveContext SaveContext )

virtual void SampleGroundTruthPositions ( float SampleTime, TArray< FVector3f >& OutPositions )

virtual void SampleGroundTruthPositionsAtFrame ( int32 FrameIndex, TArray< FVector3f >& OutPositions )

virtual void Serialize ( FArchive& Archive )

void SetAlignmentTransform ( const FTransform& Transform )

void SetAnimSequence ( UAnimSequence* AnimSeq )

void SetBoneIncludeList ( const TArray< FBoneReference >& List )

void SetCurveIncludeList ( const TArray< FMLDeformerCurveReference >& List )

void SetDeltaCutoffLength ( float Length )

void SetRecoverStrippedDataAfterCook ( bool bRecover )

void SetShouldIncludeBonesInTraining ( bool bInclude )

void SetShouldIncludeCurvesInTraining ( bool bInclude )

void SetSkeletalMesh ( USkeletalMesh* SkelMesh )

void SetTrainingDataProcessorSettings ( UMLDeformerTrainingDataProcessorSettings* Settings )

void SetTrainingDevice ( const FString& DeviceName )

void SetTrainingDeviceList ( const TArray< FString >& Devices )

void SetTrainingDeviceToCpu()

void SetTrainingFrameLimit ( int32 MaxNumFrames )

void SetVertexMap ( const TArray< int32 >& Map )

void SetVizSettings ( UMLDeformerVizSettings* VizSettingsObject )

bool ShouldIncludeBonesInTraining()

bool ShouldIncludeCurvesInTraining ()

virtual void UpdateCachedNumVertices()

virtual void UpdateMemoryUsage()

virtual void UpdateNumBaseMeshVertices ()

virtual void UpdateNumTargetMeshVertices ()

void FloatArrayToVector3Array ( const TArray< float >& FloatArray, TArray< FVector3f >& OutVectorArray )

void SetInputInfo ( UMLDeformerInputInfo* Input )

void SetNumBaseMeshVerts ( int32 NumVerts )

void SetNumTargetMeshVerts ( int32 NumVerts )

static int32 ExtractNumImportedSkinnedVertices ( const USkeletalMesh* SkeletalMesh )

static FName GetAlignmentTransformPropertyName()

static FName GetAnimSequencePropertyName()

static FName GetBoneIncludeListPropertyName()

static FName GetCurveIncludeListPropertyName()

static FName GetDeltaCutoffLengthPropertyName()

static FName GetMaxNumLODsPropertyName()

static FName GetMaxTrainingFramesPropertyName()

static FName GetShouldIncludeBonesPropertyName()

static FName GetShouldIncludeCurvesPropertyName()

static FName GetSkeletalMeshPropertyName()

static FName GetTrainingDevicePropertyName()



---

## MobileLauncherProfileWizard

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MobileLauncherProfileWizard

**Contents:**
- MobileLauncherProfileWizard
- Navigation
- Interfaces



---

## ModelingComponentsEditorOnly

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ModelingComponentsEditorOnly

**Contents:**
- ModelingComponentsEditorOnly
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Variables
  - Public



---

## ModelingComponents

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ModelingComponents

**Contents:**
- ModelingComponents
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

const TArray< int32 > & GetGroupIDs()

bool HasRenderableLines()

void MeshDebugDraw::DrawHierarchicalGrid ( double BaseGridScale, double GridZoomFactor, int32 MaxLevelDensity, const FVector& WorldMaxBounds, const FVector& WorldMinBounds, int32 Levels, int32 Subdivisions, TArray< FColor >& Colors, const FFrame3d& LocalFrame, float LineWidth, bool bDepthTested, FPrimitiveDrawInterface* PDI, const FTransform& Transform )

void MeshDebugDraw::DrawNormals ( const FDynamicMeshNormalOverlay* Overlay, float Length, FColor Color, float Thickness, bool bScreenSpace, FPrimitiveDrawInterface* PDI, const FTransform& Transform )

void MeshDebugDraw::DrawSimpleFixedScreenAreaGrid ( const FViewCameraState& CameraState, const FFrame3d& LocalFrame, int32 NumGridLines, double VisualAngleSpan, float LineWidth, FColor Color, bool bDepthTested, FPrimitiveDrawInterface* PDI, const FTransform& Transform )

void MeshDebugDraw::DrawSimpleGrid ( const FFrame3d& LocalFrame, int GridLines, double GridLineSpacing, float LineWidth, FColor Color, bool bDepthTested, FPrimitiveDrawInterface* PDI, const FTransform& Transform )

void MeshDebugDraw::DrawTriCentroids ( const FDynamicMesh3* Mesh, const TArray< int >& Indices, float PointSize, FColor Color, FPrimitiveDrawInterface* PDI, const FTransform& Transform )

void MeshDebugDraw::DrawVertices ( const FDynamicMesh3* Mesh, const TArray< int >& Indices, float PointSize, FColor Color, FPrimitiveDrawInterface* PDI, const FTransform& Transform )

void MeshDebugDraw::DrawVertices ( const FDynamicMesh3* Mesh, const TSet< int >& Indices, float PointSize, FColor Color, FPrimitiveDrawInterface* PDI, const FTransform& Transform )

bool operator! ( EEnumerateRenderCachesDirtyFlags E )

EEnumerateRenderCachesDirtyFlags operator& ( EEnumerateRenderCachesDirtyFlags Lhs, EEnumerateRenderCachesDirtyFlags Rhs )

EEnumerateRenderCachesDirtyFlags & operator&= ( EEnumerateRenderCachesDirtyFlags& Lhs, EEnumerateRenderCachesDirtyFlags Rhs )

EEnumerateRenderCachesDirtyFlags operator^ ( EEnumerateRenderCachesDirtyFlags Lhs, EEnumerateRenderCachesDirtyFlags Rhs )

EEnumerateRenderCachesDirtyFlags & operator^= ( EEnumerateRenderCachesDirtyFlags& Lhs, EEnumerateRenderCachesDirtyFlags Rhs )

EEnumerateRenderCachesDirtyFlags operator| ( EEnumerateRenderCachesDirtyFlags Lhs, EEnumerateRenderCachesDirtyFlags Rhs )

EEnumerateRenderCachesDirtyFlags & operator|= ( EEnumerateRenderCachesDirtyFlags& Lhs, EEnumerateRenderCachesDirtyFlags Rhs )

EEnumerateRenderCachesDirtyFlags operator~ ( EEnumerateRenderCachesDirtyFlags E )

bool operator== ( const FGenericMeshSelection& Other ) const

double ToolSceneQueriesUtil::CalculateDimensionFromVisualAngleD ( const UInteractiveTool* Tool, const FVector3d& Point, double TargetVisualAngleDeg )

double ToolSceneQueriesUtil::CalculateDimensionFromVisualAngleD ( const FViewCameraState& CameraState, const FVector3d& Point, double TargetVisualAngleDeg )

double ToolSceneQueriesUtil::CalculateNormalizedViewVisualAngleD ( const FViewCameraState& CameraState, const FVector3d& Point1, const FVector3d& Point2 )

double ToolSceneQueriesUtil::CalculateViewVisualAngleD ( const UInteractiveTool* Tool, const FVector3d& Point1, const FVector3d& Point2 )

double ToolSceneQueriesUtil::CalculateViewVisualAngleD ( const FViewCameraState& CameraState, const FVector3d& Point1, const FVector3d& Point2 )

bool ToolSceneQueriesUtil::FindNearestVisibleObjectHit ( UWorld* World, FHitResult& HitResultOut, const FRay& Ray, const TArray< const UPrimitiveComponent* >* IgnoreComponents, const TArray< const UPrimitiveComponent* >* InvisibleComponentsToInclude )

bool ToolSceneQueriesUtil::FindNearestVisibleObjectHit ( USceneSnappingManager* SnappingManager, FHitResult& HitResultOut, const FRay& Ray, const TArray< const UPrimitiveComponent* >* IgnoreComponents, const TArray< const UPrimitiveComponent* >* InvisibleComponentsToInclude )

bool ToolSceneQueriesUtil::FindNearestVisibleObjectHit ( const UInteractiveTool* Tool, FHitResult& HitResultOut, const FRay& Ray, const TArray< const UPrimitiveComponent* >* IgnoreComponents, const TArray< const UPrimitiveComponent* >* InvisibleComponentsToInclude )

bool ToolSceneQueriesUtil::FindNearestVisibleObjectHit ( UWorld* World, FHitResult& HitResultOut, const FVector& Start, const FVector& End, const TArray< const UPrimitiveComponent* >* IgnoreComponents, const TArray< const UPrimitiveComponent* >* InvisibleComponentsToInclude )

bool ToolSceneQueriesUtil::FindNearestVisibleObjectHit ( const UInteractiveTool* Tool, FHitResult& HitResultOut, const FVector& Start, const FVector& End, const TArray< const UPrimitiveComponent* >* IgnoreComponents, const TArray< const UPrimitiveComponent* >* InvisibleComponentsToInclude )

bool ToolSceneQueriesUtil::FindSceneSnapPoint ( FFindSceneSnapPointParams& Params )

bool ToolSceneQueriesUtil::FindSceneSnapPoint ( const UInteractiveTool* Tool, const FVector3d& Point, FVector3d& SnapPointOut, bool bVertices, bool bEdges, double VisualAngleThreshold, FSnapGeometry* SnapGeometry, FVector* DebugTriangleOut )

bool ToolSceneQueriesUtil::FindWorldGridSnapPoint ( const UInteractiveTool* Tool, const FVector3d& QueryPoint, FVector3d& GridSnapPointOut )

double ToolSceneQueriesUtil::GetDefaultVisualAngleSnapThreshD()

bool ToolSceneQueriesUtil::IsPointVisible ( const FViewCameraState& CameraState, const FVector3d& Point )

bool ToolSceneQueriesUtil::IsVisibleObjectHit ( const FHitResult& HitResult )

double ToolSceneQueriesUtil::PointSnapMetric ( const FViewCameraState& CameraState, const FVector3d& Point1, const FVector3d& Point2 )

bool ToolSceneQueriesUtil::PointSnapQuery ( const UInteractiveTool* Tool, const FVector3d& Point1, const FVector3d& Point2, double VisualAngleThreshold )

bool ToolSceneQueriesUtil::PointSnapQuery ( const FViewCameraState& CameraState, const FVector3d& Point1, const FVector3d& Point2, double VisualAngleThreshold )

double ToolSceneQueriesUtil::SnapDistanceToWorldGridSize ( const UInteractiveTool* Tool, const double Distance )

Please use the function of the same name which takes EEnumerateSelectionMapping flags instead bool ToolSelectionUtil::AccumulateSelectionElements ( UE::Geometry::FGeometrySelectionElements& Elements, const UE::Geometry::FGeometrySelection& Selection, const UE::Geometry::FDynamicMesh3& SourceMesh, const UE::Geometry::FGroupTopology* Topology, const FTransform* ApplyTransform, bool bMapFacesToEdges )

bool ToolSelectionUtil::AccumulateSelectionElements ( UE::Geometry::FGeometrySelectionElements& Elements, const UE::Geometry::FGeometrySelection& Selection, const UE::Geometry::FDynamicMesh3& SourceMesh, const UE::Geometry::FGroupTopology* Topology, const FTransform* ApplyTransform, const UE::Geometry::EEnumerateSelectionMapping Flags )

void ToolSelectionUtil::DebugRender ( IToolsContextRenderAPI* RenderAPI, const UE::Geometry::FGeometrySelectionElements& Elements, float LineThickness, FLinearColor LineColor, float PointSize, FLinearColor PointColor, float DepthBias, FLinearColor FillColor )

void ToolSelectionUtil::DebugRenderGeometrySelectionElements ( IToolsContextRenderAPI* RenderAPI, const UE::Geometry::FGeometrySelectionElements& Elements, bool bIsPreview )

void ToolSelectionUtil::SetNewActorSelection ( UInteractiveToolManager* ToolManager, AActor* Actor )

void ToolSelectionUtil::SetNewActorSelection ( UInteractiveToolManager* ToolManager, const TArray< AActor* >& Actors )

void ToolSetupUtil::ApplyRenderingConfigurationToPreview ( UBaseDynamicMeshComponent* Component, UToolTarget* SourceTarget )

void ToolSetupUtil::ApplyRenderingConfigurationToPreview ( UPreviewMesh* PreviewMesh, UToolTarget* SourceTarget )

UCurveFloat * ToolSetupUtil::GetContrastAdjustmentCurve ( UInteractiveToolManager* ToolManager )

UMaterialInstanceDynamic * ToolSetupUtil::GetCustomDepthOffsetMaterial ( UInteractiveToolManager* ToolManager, const FLinearColor& Color, float DepthBias )

UMaterialInstanceDynamic * ToolSetupUtil::GetCustomDepthOffsetMaterial ( UInteractiveToolManager* ToolManager, const FLinearColor& Color, float DepthBias, float Opacity )

UMaterialInstanceDynamic * ToolSetupUtil::GetCustomImageBasedSculptMaterial ( UInteractiveToolManager* ToolManager, UTexture* SetImage )

UMaterialInstanceDynamic * ToolSetupUtil::GetCustomTwoSidedDepthOffsetMaterial ( UInteractiveToolManager* ToolManager, const FLinearColor& Color, float DepthBias )

UMaterialInstanceDynamic * ToolSetupUtil::GetCustomTwoSidedDepthOffsetMaterial ( UInteractiveToolManager* ToolManager, const FLinearColor& Color, float DepthBias, float Opacity )

UMaterialInstanceDynamic * ToolSetupUtil::GetDefaultBrushAlphaMaterial ( UInteractiveToolManager* ToolManager )

UMaterialInstanceDynamic * ToolSetupUtil::GetDefaultBrushVolumeMaterial ( UInteractiveToolManager* ToolManager )

UMaterialInterface * ToolSetupUtil::GetDefaultEditVolumeMaterial()

UMaterialInstanceDynamic * ToolSetupUtil::GetDefaultErrorMaterial ( UInteractiveToolManager* ToolManager )

UMaterialInterface * ToolSetupUtil::GetDefaultLineComponentMaterial ( UInteractiveToolManager* ToolManager, bool bDepthTested )

UMaterialInterface * ToolSetupUtil::GetDefaultMaterial ()

UMaterialInterface * ToolSetupUtil::GetDefaultMaterial ( UInteractiveToolManager* ToolManager, UMaterialInterface* SourceMaterial )

UMaterialInterface * ToolSetupUtil::GetDefaultPointComponentMaterial ( UInteractiveToolManager* ToolManager, bool bDepthTested )

UMaterialInterface * ToolSetupUtil::GetDefaultSculptMaterial ( UInteractiveToolManager* ToolManager )

UMaterialInterface * ToolSetupUtil::GetDefaultWorkingMaterial ( UInteractiveToolManager* ToolManager )

UMaterialInstanceDynamic * ToolSetupUtil::GetDefaultWorkingMaterialInstance ( UInteractiveToolManager* ToolManager )

UE::Geometry::FFrame3d ToolSetupUtil::GetDefaultWorldReferenceFrame ( UInteractiveToolManager* ToolManager, UE::Geometry::FQuaterniond DefaultOrientation, double NoSelectionPlacementDistance )

UMaterialInterface * ToolSetupUtil::GetImageBasedSculptMaterial ( UInteractiveToolManager* ToolManager, ImageMaterialType Type )

UMaterialInterface * ToolSetupUtil::GetRoundPointComponentMaterial ( UInteractiveToolManager* ToolManager, bool bDepthTested )

UMaterialInterface * ToolSetupUtil::GetSelectionMaterial ( UInteractiveToolManager* ToolManager )

UMaterialInterface * ToolSetupUtil::GetSelectionMaterial ( const FLinearColor& UseColor, UInteractiveToolManager* ToolManager, float DepthBias )

UMaterialInstanceDynamic * ToolSetupUtil::GetSimpleCustomMaterial ( UInteractiveToolManager* ToolManager, const FLinearColor& Color )

UMaterialInstanceDynamic * ToolSetupUtil::GetSimpleCustomMaterial ( UInteractiveToolManager* ToolManager, const FLinearColor& Color, float Opacity )

UMaterialInstanceDynamic * ToolSetupUtil::GetTransparentSculptMaterial ( UInteractiveToolManager* ToolManager, const FLinearColor& Color, double Opacity, bool bTwoSided )

UMaterialInstanceDynamic * ToolSetupUtil::GetUVCheckerboardMaterial ( double CheckerDensity )

UMaterialInstanceDynamic * ToolSetupUtil::GetVertexColorMaterial ( UInteractiveToolManager* ToolManager, bool bTwoSided )

UMaterialInterface * ToolSetupUtil::GetVertexColorSculptMaterial ( UInteractiveToolManager* ToolManager )

bool UE::AssetUtils::ConvertToSingleChannel ( UTexture2D* TextureMap )

bool UE::AssetUtils::ForceVirtualTexturePrefetch ( FImageDimensions ScreenSpaceDimensions, bool bWaitForPrefetchToComplete )

FName UE::AssetUtils::GenerateNewMaterialSlotName ( const TArray< FStaticMaterial >& ExistingMaterials, UMaterialInterface* SlotMaterial, int32 NewSlotIndex )

bool UE::AssetUtils::GetStaticMeshLODAssetMaterials ( UStaticMesh* StaticMeshAsset, int32 LODIndex, FStaticMeshLODMaterialSetInfo& MaterialInfoOut )

bool UE::AssetUtils::GetStaticMeshLODMaterialListBySection ( UStaticMesh* StaticMeshAsset, int32 LODIndex, TArray< UMaterialInterface* >& MaterialListOut, TArray< int32 >& MaterialIndexOut, TArray< FName >& MaterialSlotNameOut )

bool UE::AssetUtils::ReadTexture ( UTexture2D* TextureMap, TImageBuilder< FVector4f >& DestImageOut, const bool bPreferPlatformData )

bool UE::AssetUtils::SaveDebugImage ( const TArray< FColor >& Pixels, FImageDimensions Dimensions, FString DebugSubfolder, FString FilenameBase, int32 UseFileCounter )

bool UE::AssetUtils::SaveDebugImage ( const FImageAdapter& Image, bool bConvertToSRGB, FString DebugSubfolder, FString FilenameBase, int32 UseFileCounter )

bool UE::AssetUtils::SaveDebugImage ( const TArray< FLinearColor >& Pixels, FImageDimensions Dimensions, bool bConvertToSRGB, FString DebugSubfolder, FString FilenameBase, int32 UseFileCounter )

void UE::Geometry::SplineUtil::DrawSpline ( const USplineComponent& SplineComp, IToolsContextRenderAPI& RenderAPI, const FDrawSplineSettings& Settings )

void UE::Geometry::SplineUtil::ProjectSplineToSurface ( FInterpCurveVector& OutputSpline, const FInterpCurveVector& InputSpline, const UE::Geometry::FDynamicMeshAABBTree3& SurfaceAABBTree, const FTransform& SplineTransform, const FTransform& MeshTransform, double RelativeErrorThreshold, int32 MaxNewPoints )

void UE::MeshDescription::ConfigureBuildSettings ( UStaticMesh* StaticMesh, int32 SourceLOD, FStaticMeshBuildSettingChange NewSettings )

void UE::MeshDescription::InitializeAutoGeneratedAttributes ( FMeshDescription& Mesh, const FMeshBuildSettings* BuildSettings )

void UE::MeshDescription::InitializeAutoGeneratedAttributes ( FMeshDescription& Mesh, UStaticMesh* StaticMesh, int32 SourceLOD )

void UE::MeshDescription::InitializeAutoGeneratedAttributes ( FMeshDescription& Mesh, UActorComponent* StaticMeshComponent, int32 SourceLOD )

FCreateMaterialObjectResult UE::Modeling::CreateMaterialObject ( UInteractiveToolManager* ToolManager, FCreateMaterialObjectParams&& CreateMaterialParams )

FCreateMeshObjectResult UE::Modeling::CreateMeshObject ( UInteractiveToolManager* ToolManager, FCreateMeshObjectParams&& CreateMeshParams )

FCreateActorResult UE::Modeling::CreateNewActor ( UInteractiveToolManager* ToolManager, FCreateActorParams&& CreateActorParams )

FCreateComponentResult UE::Modeling::CreateNewComponentOnActor ( UInteractiveToolManager* ToolManager, FCreateComponentParams&& CreateComponentParams )

FCreateTextureObjectResult UE::Modeling::CreateTextureObject ( UInteractiveToolManager* ToolManager, FCreateTextureObjectParams&& CreateTexParams )

FString UE::Modeling::GenerateRandomShortHexString ( int32 NumChars )

FString UE::Modeling::GetComponentAssetBaseName ( UActorComponent* Component, bool bRemoveAutoGeneratedSuffixes )

FString UE::Modeling::StripGeneratedAssetSuffixFromName ( FString InputName )

bool UE::ToolTarget::ApplyIncrementalMeshEditChange ( UToolTarget* Target, TFunctionRef< bool(UE::Geometry::FDynamicMesh3&EditMesh, UObject*TransactionTarget)> MeshEditi... )

EDynamicMeshUpdateResult UE::ToolTarget::CommitDynamicMeshNormalsUpdate ( UToolTarget* Target, const UE::Geometry::FDynamicMesh3* UpdatedMesh, bool bUpdateTangents )

EDynamicMeshUpdateResult UE::ToolTarget::CommitDynamicMeshUpdate ( UToolTarget* Target, const UE::Geometry::FDynamicMesh3& UpdatedMesh, bool bHaveModifiedTopology, const FConversionToMeshDescriptionOptions& ConversionOptions, const FComponentMaterialSet* UpdatedMaterials )

EDynamicMeshUpdateResult UE::ToolTarget::CommitDynamicMeshUVUpdate ( UToolTarget* Target, const UE::Geometry::FDynamicMesh3* UpdatedMesh )

bool UE::ToolTarget::CommitMaterialSetUpdate ( UToolTarget* Target, const FComponentMaterialSet& UpdatedMaterials, bool bApplyToAsset )

EDynamicMeshUpdateResult UE::ToolTarget::CommitMeshDescriptionUpdate ( UToolTarget* Target, FMeshDescription&& UpdatedMesh, const FCommitMeshParameters& CommitParams )

EDynamicMeshUpdateResult UE::ToolTarget::CommitMeshDescriptionUpdate ( UToolTarget* Target, const FMeshDescription* UpdatedMesh, const FComponentMaterialSet* UpdatedMaterials, const FCommitMeshParameters& CommitParams )

EDynamicMeshUpdateResult UE::ToolTarget::CommitMeshDescriptionUpdateViaDynamicMesh ( UToolTarget* Target, const UE::Geometry::FDynamicMesh3& UpdatedMesh, bool bHaveModifiedTopology, const FCommitMeshParameters& CommitParams )

bool UE::ToolTarget::ConfigureCreateMeshObjectParams ( UToolTarget* SourceTarget, FCreateMeshObjectParams& DerivedParamsOut )

UE::Geometry::FDynamicMesh3 UE::ToolTarget::GetDynamicMeshCopy ( UToolTarget* Target, bool bWantMeshTangents )

UE::Geometry::FDynamicMesh3 UE::ToolTarget::GetDynamicMeshCopy ( UToolTarget* Target, const FGetMeshParameters& InGetMeshParams )

FMeshDescription UE::ToolTarget::GetEmptyMeshDescription ( UToolTarget* Target )

FString UE::ToolTarget::GetHumanReadableName ( UToolTarget* Target )

FTransform3d UE::ToolTarget::GetLocalToWorldTransform ( UToolTarget* Target )

FComponentMaterialSet UE::ToolTarget::GetMaterialSet ( UToolTarget* Target, bool bPreferAssetMaterials )

const FMeshDescription * UE::ToolTarget::GetMeshDescription ( UToolTarget* Target, const FGetMeshParameters& GetMeshParams )

FMeshDescription UE::ToolTarget::GetMeshDescriptionCopy ( UToolTarget* Target, const FGetMeshParameters& GetMeshParams )

TArray< EMeshLODIdentifier > UE::ToolTarget::GetMeshDescriptionLODs ( UToolTarget* Target, bool& bOutTargetSupportsLODs, bool bOnlyReturnDefaultLOD, bool bExcludeAutoGeneratedLODs )

UBodySetup * UE::ToolTarget::GetPhysicsBodySetup ( UToolTarget* Target )

IInterface_CollisionDataProvider * UE::ToolTarget::GetPhysicsCollisionDataProvider ( UToolTarget* Target )

USkeletalMesh * UE::ToolTarget::GetSkeletalMeshFromTargetIfAvailable ( UToolTarget* Target )

UStaticMesh * UE::ToolTarget::GetStaticMeshFromTargetIfAvailable ( UToolTarget* Target )

AActor * UE::ToolTarget::GetTargetActor ( UToolTarget* Target )

UPrimitiveComponent * UE::ToolTarget::GetTargetComponent ( UToolTarget* Target )

EMeshLODIdentifier UE::ToolTarget::GetTargetMeshDescriptionLOD ( UToolTarget* Target, bool& bOutTargetSupportsLODs )

USceneComponent * UE::ToolTarget::GetTargetSceneComponent ( UToolTarget* Target )

int32 UE::ToolTarget::GetTriangleCount ( UToolTarget* Target )

bool UE::ToolTarget::HideSourceObject ( UToolTarget* Target )

void UE::ToolTarget::Internal::CommitDynamicMeshViaIPersistentDynamicMeshSource ( IPersistentDynamicMeshSource& DynamicMeshSource, const UE::Geometry::FDynamicMesh3& UpdatedMesh, bool bHaveModifiedTopology )

void UE::ToolTarget::Internal::PostEditChangeWithConditionalUndo ( UObject* Object )

void UE::ToolTarget::SafeDeleteActor ( AActor* TargetActor )

bool UE::ToolTarget::SetSourceObjectVisible ( UToolTarget* Target, bool bVisible )

bool UE::ToolTarget::ShowSourceObject ( UToolTarget* Target )

bool UE::ToolTarget::SupportsIncrementalMeshChanges ( UToolTarget* Target )

void UE::WeightMaps::FindVertexWeightMaps ( const FMeshDescription* Mesh, TArray< FName >& PropertyNamesOut )

bool UE::WeightMaps::GetVertexWeightMap ( const FMeshDescription* Mesh, FName AttributeName, FIndexedWeightMap1f& WeightMap, float DefaultValue )



---

## ModelingEditorUI

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ModelingEditorUI

**Contents:**
- ModelingEditorUI
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

TSharedRef< SCheckBox > UE::ModelingUI::MakeBoolToggleButton ( TSharedPtr< IPropertyHandle > BoolToggleHandle, FText ButtonLabelText, TFunction< void(bool)> ToggledCallback, int HorzPadding )

TSharedRef< SHorizontalBox > UE::ModelingUI::MakeFixedWidthLabelSliderHBox ( TSharedPtr< IPropertyHandle > LabelHandle, TSharedPtr< SDynamicNumericEntry::FDataSource > SliderDataSource, int32 LabelFixedWidth )

TSharedRef< SHorizontalBox > UE::ModelingUI::MakeToggleSliderHBox ( TSharedPtr< IPropertyHandle > BoolToggleHandle, FText ToggleLabelText, TSharedPtr< SDynamicNumericEntry::FDataSource > SliderDataSource, int32 ToggleFixedWidth )

TSharedRef< SHorizontalBox > UE::ModelingUI::MakeTwoWidgetDetailRowHBox ( TSharedRef< SWidget > Widget1, TSharedRef< SWidget > Widget2, float FillWidth1, float FillWidth2 )

void UE::ModelingUI::ProcessChildWidgetsByType ( const TSharedRef< SWidget >& RootWidget, const FString& WidgetType, TFunction< bool(TSharedRef< SWidget >&)> ProcessFunc )

void UE::ModelingUI::SetCustomWidgetErrorString ( FText ErrorString, SlotType& Slot )

TSharedRef< SBox > UE::ModelingUI::WrapInFixedWidthBox ( TSharedRef< SWidget > SubWidget, int32 Width )



---

## ModelingOperatorsEditorOnly

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ModelingOperatorsEditorOnly

**Contents:**
- ModelingOperatorsEditorOnly
- Navigation
- Classes
- Enums
  - Public



---

## ModelingOperators

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ModelingOperators

**Contents:**
- ModelingOperators
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## ModelingToolsEditorMode

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ModelingToolsEditorMode

**Contents:**
- ModelingToolsEditorMode
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

bool UE::Modeling::AutoSaveAsset ( UObject* Asset )

FString UE::Modeling::GetGlobalAssetRootPath()

FString UE::Modeling::GetNewAssetPathName ( const FString& BaseName, const UWorld* TargetWorld, FString SuggestedFolder )

FString UE::Modeling::GetWorldRelativeAssetRootPath ( const UWorld* World )

void UE::Modeling::OnNewAssetCreated ( UObject* Asset )



---

## ModelingUI

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ModelingUI

**Contents:**
- ModelingUI
- Navigation
- Classes



---

## ModelViewViewModelBlueprint

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ModelViewViewModelBlueprint

**Contents:**
- ModelViewViewModelBlueprint
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

bool operator! ( EFilterFlag E )

EFilterFlag operator& ( EFilterFlag Lhs, EFilterFlag Rhs )

EFilterFlag & operator&= ( EFilterFlag& Lhs, EFilterFlag Rhs )

EFilterFlag operator^ ( EFilterFlag Lhs, EFilterFlag Rhs )

EFilterFlag & operator^= ( EFilterFlag& Lhs, EFilterFlag Rhs )

EFilterFlag operator| ( EFilterFlag Lhs, EFilterFlag Rhs )

EFilterFlag & operator|= ( EFilterFlag& Lhs, EFilterFlag Rhs )

EFilterFlag operator~ ( EFilterFlag E )



---

## ModelViewViewModelDebugger

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ModelViewViewModelDebugger

**Contents:**
- ModelViewViewModelDebugger
- Navigation
- Classes
- Structs



---

## ModelViewViewModelEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ModelViewViewModelEditor

**Contents:**
- ModelViewViewModelEditor
- Navigation
- Classes
- Structs



---

## ModelViewViewModel

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ModelViewViewModel

**Contents:**
- ModelViewViewModel
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

const TCHAR * LexToString ( EMVVMConditionOperation Enum )



---

## ModularGameplay

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ModularGameplay

**Contents:**
- ModularGameplay
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

bool operator! ( EGameFrameworkAddComponentFlags E )

EGameFrameworkAddComponentFlags operator& ( EGameFrameworkAddComponentFlags Lhs, EGameFrameworkAddComponentFlags Rhs )

EGameFrameworkAddComponentFlags & operator&= ( EGameFrameworkAddComponentFlags& Lhs, EGameFrameworkAddComponentFlags Rhs )

EGameFrameworkAddComponentFlags operator^ ( EGameFrameworkAddComponentFlags Lhs, EGameFrameworkAddComponentFlags Rhs )

EGameFrameworkAddComponentFlags & operator^= ( EGameFrameworkAddComponentFlags& Lhs, EGameFrameworkAddComponentFlags Rhs )

EGameFrameworkAddComponentFlags operator| ( EGameFrameworkAddComponentFlags Lhs, EGameFrameworkAddComponentFlags Rhs )

EGameFrameworkAddComponentFlags & operator|= ( EGameFrameworkAddComponentFlags& Lhs, EGameFrameworkAddComponentFlags Rhs )

EGameFrameworkAddComponentFlags operator~ ( EGameFrameworkAddComponentFlags E )



---

## MotionTrajectory

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MotionTrajectory

**Contents:**
- MotionTrajectory
- Navigation
- Classes
- Structs



---

## MotionWarping

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MotionWarping

**Contents:**
- MotionWarping
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public



---

## MotorSimOutputMotoSynth

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MotorSimOutputMotoSynth

**Contents:**
- MotorSimOutputMotoSynth
- Navigation
- Classes



---

## MotoSynthEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MotoSynthEditor

**Contents:**
- MotoSynthEditor
- Navigation
- Classes



---

## MotoSynth

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MotoSynth

**Contents:**
- MotoSynth
- Navigation
- Classes
- Structs
- Interfaces



---

## MoverAnimNext

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MoverAnimNext

**Contents:**
- MoverAnimNext
- Navigation
- Classes



---

## MoverCVDData

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MoverCVDData

**Contents:**
- MoverCVDData
- Navigation
- Structs
- Functions
  - Public

CVD_IMPLEMENT_SERIALIZER ( FMoverCVDSimDataWrapper )



---

## MoverCVDEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MoverCVDEditor

**Contents:**
- MoverCVDEditor
- Navigation
- Classes



---

## MoverEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MoverEditor

**Contents:**
- MoverEditor
- Navigation
- Classes



---

## MoverExamples

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MoverExamples

**Contents:**
- MoverExamples
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Variables
  - Public



---

## MoverIntegrations

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MoverIntegrations

**Contents:**
- MoverIntegrations
- Navigation
- Classes



---

## MoverMassIntegration

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MoverMassIntegration

**Contents:**
- MoverMassIntegration
- Navigation
- Classes
- Structs



---

## MoverTests

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MoverTests

**Contents:**
- MoverTests
- Navigation
- Classes
- Structs



---

## Mover

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Mover

**Contents:**
- Mover
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

bool operator! ( EPatternAxisMaskFlags E )

EPatternAxisMaskFlags operator& ( EPatternAxisMaskFlags Lhs, EPatternAxisMaskFlags Rhs )

EPatternAxisMaskFlags & operator&= ( EPatternAxisMaskFlags& Lhs, EPatternAxisMaskFlags Rhs )

EPatternAxisMaskFlags operator^ ( EPatternAxisMaskFlags Lhs, EPatternAxisMaskFlags Rhs )

EPatternAxisMaskFlags & operator^= ( EPatternAxisMaskFlags& Lhs, EPatternAxisMaskFlags Rhs )

EPatternAxisMaskFlags operator| ( EPatternAxisMaskFlags Lhs, EPatternAxisMaskFlags Rhs )

EPatternAxisMaskFlags & operator|= ( EPatternAxisMaskFlags& Lhs, EPatternAxisMaskFlags Rhs )

EPatternAxisMaskFlags operator~ ( EPatternAxisMaskFlags E )



---

## MoviePipelineMaskRenderPass

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MoviePipelineMaskRenderPass

**Contents:**
- MoviePipelineMaskRenderPass
- Navigation
- Classes
- Structs



---

## MovieRenderPipelineCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MovieRenderPipelineCore

**Contents:**
- MovieRenderPipelineCore
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

FString LexToString ( const FMovieGraphNamedResolution InResolution )

bool operator! ( EMovieGraphQuickRenderViewportLookFlags E )

EMovieGraphQuickRenderViewportLookFlags operator& ( EMovieGraphQuickRenderViewportLookFlags Lhs, EMovieGraphQuickRenderViewportLookFlags Rhs )

EMovieGraphQuickRenderViewportLookFlags & operator&= ( EMovieGraphQuickRenderViewportLookFlags& Lhs, EMovieGraphQuickRenderViewportLookFlags Rhs )

EMovieGraphQuickRenderViewportLookFlags operator^ ( EMovieGraphQuickRenderViewportLookFlags Lhs, EMovieGraphQuickRenderViewportLookFlags Rhs )

EMovieGraphQuickRenderViewportLookFlags & operator^= ( EMovieGraphQuickRenderViewportLookFlags& Lhs, EMovieGraphQuickRenderViewportLookFlags Rhs )

EMovieGraphQuickRenderViewportLookFlags operator| ( EMovieGraphQuickRenderViewportLookFlags Lhs, EMovieGraphQuickRenderViewportLookFlags Rhs )

EMovieGraphQuickRenderViewportLookFlags & operator|= ( EMovieGraphQuickRenderViewportLookFlags& Lhs, EMovieGraphQuickRenderViewportLookFlags Rhs )

EMovieGraphQuickRenderViewportLookFlags operator~ ( EMovieGraphQuickRenderViewportLookFlags E )

bool UE::MovieGraph::Private::GetOptionalValue ( TValueOrError< ReturnType, EPropertyBagResult >& PropertyBagValue, ReturnType& OutValue )

void UE::MoviePipeline::DoPostProcessBlend ( const FVector& InViewLocation, const UWorld* InWorld, const FMinimalViewInfo& InViewInfo, FSceneView* InOutView )

static UWorld * MoviePipeline::FindCurrentWorld()

static FLinearColor UE::MoviePipeline::GetColorBilinearFiltered ( const FImagePixelData* InSampleData, const FVector2D& InSamplePixelCoords, bool& OutClipped, bool bInForceAlphaToOpaque )

static FLinearColor UE::MoviePipeline::GetColorCubicFiltered ( const FImagePixelData* InSampleData, const FVector2D& InSamplePixelCoords, float CubicBParam, float CubicCParam, bool& OutClipped, bool bInForceAlphaToOpaque )



---

## MovieRenderPipelineEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MovieRenderPipelineEditor

**Contents:**
- MovieRenderPipelineEditor
- Navigation
- Classes
- Interfaces
- Typedefs



---

## MovieRenderPipelineMP4Encoder

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MovieRenderPipelineMP4Encoder

**Contents:**
- MovieRenderPipelineMP4Encoder
- Navigation
- Classes



---

## MovieRenderPipelineRenderPasses

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MovieRenderPipelineRenderPasses

**Contents:**
- MovieRenderPipelineRenderPasses
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## MovieRenderPipelineSettings

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MovieRenderPipelineSettings

**Contents:**
- MovieRenderPipelineSettings
- Navigation
- Classes



---

## MovieSceneAnimMixerEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MovieSceneAnimMixerEditor

**Contents:**
- MovieSceneAnimMixerEditor
- Navigation
- Classes



---

## MovieSceneAnimMixer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MovieSceneAnimMixer

**Contents:**
- MovieSceneAnimMixer
- Navigation
- Classes
- Structs
- Typedefs
- Functions
  - Public

bool operator! ( FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions E )

FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions operator& ( FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions Lhs, FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions Rhs )

FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions & operator&= ( FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions& Lhs, FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions Rhs )

FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions operator^ ( FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions Lhs, FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions Rhs )

FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions & operator^= ( FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions& Lhs, FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions Rhs )

FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions operator| ( FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions Lhs, FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions Rhs )

FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions & operator|= ( FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions& Lhs, FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions Rhs )

FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions operator~ ( FAnimNextConvertRootMotionToWorldSpaceTask::ESpaceConversions E )



---

## MovieScenePoseSearchTracks

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MovieScenePoseSearchTracks

**Contents:**
- MovieScenePoseSearchTracks
- Navigation
- Classes
- Structs



---

## MovieSceneTextTrack

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MovieSceneTextTrack

**Contents:**
- MovieSceneTextTrack
- Navigation



---

## MQTTCoreEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MQTTCoreEditor

**Contents:**
- MQTTCoreEditor
- Navigation
- Interfaces



---

## MQTTCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MQTTCore

**Contents:**
- MQTTCore
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Constants
- Functions
  - Public

uint32 GetTypeHash ( const IMQTTClient& InClient )

uint32 GetTypeHash ( const FMQTTURL& InURL )



---

## MsQuicRuntime

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MsQuicRuntime

**Contents:**
- MsQuicRuntime
- Navigation
- Classes



---

## MultiServerConfiguration

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MultiServerConfiguration

**Contents:**
- MultiServerConfiguration
- Navigation
- Classes



---

## MultiServerReplication

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MultiServerReplication

**Contents:**
- MultiServerReplication
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public



---

## MultiUserClientLibrary

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MultiUserClientLibrary

**Contents:**
- MultiUserClientLibrary
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## MultiUserClient

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MultiUserClient

**Contents:**
- MultiUserClient
- Navigation
- Structs
- Interfaces
- Enums
  - Public



---

## MultiUserServer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MultiUserServer

**Contents:**
- MultiUserServer
- Navigation
- Interfaces



---

## MusicEnvironmentEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MusicEnvironmentEditor

**Contents:**
- MusicEnvironmentEditor
- Navigation
- Classes



---

## MusicEnvironment

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MusicEnvironment

**Contents:**
- MusicEnvironment
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## MutableDataflowEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/MutableDataflowEditor

**Contents:**
- MutableDataflowEditor
- Navigation
- Classes
- Structs



---

## NamingTokensUI

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NamingTokensUI

**Contents:**
- NamingTokensUI
- Navigation
- Classes



---

## NamingTokens

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NamingTokens

**Contents:**
- NamingTokens
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Variables
  - Public
- Functions
  - Public

FString UE::NamingTokens::Utils::CombineNamespaceAndTokenKey ( const FString& InNamespace, const FString& InTokenKey )

FString UE::NamingTokens::Utils::CreateFormattedToken ( const FNamingTokenData& InToken )

FString UE::NamingTokens::Utils::GetNamespaceDelimiter()

FString UE::NamingTokens::Utils::GetNamespaceFromTokenKey ( const FString& InTokenKey )

UFunction * UE::NamingTokens::Utils::GetProcessTokenFunctionSignature()

TArray< FString > UE::NamingTokens::Utils::GetTokenKeysFromString ( const FString& InTokenString )

bool UE::NamingTokens::Utils::IsTokenInString ( const FString& InTokenKey, const FString& InTokenString )

FString UE::NamingTokens::Utils::RemoveNamespaceFromTokenKey ( const FString& InTokenKey )

bool UE::NamingTokens::Utils::ValidateName ( const FString& InName, FText& OutErrorMessage )

bool UE::NamingTokens::Utils::ValidateTokenFunction ( const UFunction* InFunction )



---

## NaniteAssemblyEditorUtils

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NaniteAssemblyEditorUtils

**Contents:**
- NaniteAssemblyEditorUtils
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## NaniteDisplacedMeshEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NaniteDisplacedMeshEditor

**Contents:**
- NaniteDisplacedMeshEditor
- Navigation
- Classes
- Structs
- Enums
  - Public
- Variables
  - Public
- Functions
  - Public

FString GenerateLinkedDisplacedMeshAssetName ( const FNaniteDisplacedMeshParams& InParameters )

FGuid GetAggregatedId ( const FNaniteDisplacedMeshParams& DisplacedMeshParams )

FGuid GetAggregatedId ( const UNaniteDisplacedMesh& DisplacedMesh )

FString GetAggregatedIdString ( const FNaniteDisplacedMeshParams& DisplacedMeshParams )

FString GetAggregatedIdString ( const UNaniteDisplacedMesh& DisplacedMesh )

FString GetSuggestedDisplacedMeshFolder ( const FStringView& InSubPathForDisplacedMesh, const FValidatedNaniteDisplacedMeshParams& InParameters )

UNaniteDisplacedMesh * LinkDisplacedMeshAsset ( UNaniteDisplacedMesh* ExistingDisplacedMesh, FValidatedNaniteDisplacedMeshParams&& InParameters, const FNaniteDisplacedMeshLinkParameters& InLinkParameters )

UNaniteDisplacedMesh * LinkDisplacedMeshAsset ( UNaniteDisplacedMesh* ExistingDisplacedMesh, const FNaniteDisplacedMeshParams& InParameters, const FString& DisplacedMeshFolder, ELinkDisplacedMeshAssetSetting LinkDisplacedMeshAssetSetting, bool* bOutCreatedNewMesh )



---

## NaniteDisplacedMesh

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NaniteDisplacedMesh

**Contents:**
- NaniteDisplacedMesh
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

bool DisplaceNaniteMesh ( const FNaniteDisplacedMeshParams& Parameters, const uint32 NumTextureCoord, FMeshBuildVertexData& Verts, TArray< uint32 >& Indexes, TArray< int32 >& MaterialIndexes, FBounds3f& VertexBounds, EDisplaceNaniteMeshOptions::Type Options )



---

## NavCorridor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NavCorridor

**Contents:**
- NavCorridor
- Navigation
- Classes
- Structs



---

## NDIMedia

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NDIMedia

**Contents:**
- NDIMedia
- Navigation
- Classes
- Enums
  - Public



---

## NearestNeighborModelEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NearestNeighborModelEditor

**Contents:**
- NearestNeighborModelEditor
- Navigation
- Classes
- Enums
  - Public



---

## NearestNeighborModel

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NearestNeighborModel

**Contents:**
- NearestNeighborModel
- Navigation
- Classes
- Enums
  - Public
- Variables
  - Public



---

## NetcodeUnitTest

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NetcodeUnitTest

**Contents:**
- NetcodeUnitTest
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

Globals | UnitLogging.h | |

Globals | NetcodeUnitTest.h | |

Globals | NUTUtilDebug.h | |

EMinClientFlags FromUnitTestFlags ( EUnitTestFlags Flags )

int32 GetUnitTaskPriority ( EUnitTaskFlags InFlags )

FString GetUnitTestFlagName ( EUnitTestFlags Flag )

FString GetUnitTestResetStageName ( EUnitTestResetStage Stage )

bool GGlobalExec ( UWorld* InWorld, const TCHAR* Cmd, FOutputDevice& Ar )

TSharedRef< SWindow > OpenLogDialog_NonModal ( EAppMsgType::Type InMessageType, const FText& InMessage, const FText& InTitle, FOnLogDialogResult ResultCallback )

TSharedRef< SWindow > OpenLogDialog_NonModal ( EAppMsgType::Type InMessageType, const FString& InMessage, const FString& InTitle, FOnLogDialogResult ResultCallback )

bool operator! ( EUnitTaskFlags E )

bool operator! ( EMinClientFlags E )

bool operator! ( EUnitTestFlags E )

bool operator! ( ELogTraceFlags E )

bool operator! ( ELogType E )

EUnitTaskFlags operator& ( EUnitTaskFlags Lhs, EUnitTaskFlags Rhs )

EMinClientFlags operator& ( EMinClientFlags Lhs, EMinClientFlags Rhs )

EUnitTestFlags operator& ( EUnitTestFlags Lhs, EUnitTestFlags Rhs )

ELogTraceFlags operator& ( ELogTraceFlags Lhs, ELogTraceFlags Rhs )

ELogType operator& ( ELogType Lhs, ELogType Rhs )

EUnitTaskFlags & operator&= ( EUnitTaskFlags& Lhs, EUnitTaskFlags Rhs )

EMinClientFlags & operator&= ( EMinClientFlags& Lhs, EMinClientFlags Rhs )

EUnitTestFlags & operator&= ( EUnitTestFlags& Lhs, EUnitTestFlags Rhs )

ELogTraceFlags & operator&= ( ELogTraceFlags& Lhs, ELogTraceFlags Rhs )

ELogType & operator&= ( ELogType& Lhs, ELogType Rhs )

EUnitTaskFlags operator^ ( EUnitTaskFlags Lhs, EUnitTaskFlags Rhs )

EMinClientFlags operator^ ( EMinClientFlags Lhs, EMinClientFlags Rhs )

EUnitTestFlags operator^ ( EUnitTestFlags Lhs, EUnitTestFlags Rhs )

ELogTraceFlags operator^ ( ELogTraceFlags Lhs, ELogTraceFlags Rhs )

ELogType operator^ ( ELogType Lhs, ELogType Rhs )

EUnitTaskFlags & operator^= ( EUnitTaskFlags& Lhs, EUnitTaskFlags Rhs )

EMinClientFlags & operator^= ( EMinClientFlags& Lhs, EMinClientFlags Rhs )

EUnitTestFlags & operator^= ( EUnitTestFlags& Lhs, EUnitTestFlags Rhs )

ELogTraceFlags & operator^= ( ELogTraceFlags& Lhs, ELogTraceFlags Rhs )

ELogType & operator^= ( ELogType& Lhs, ELogType Rhs )

EUnitTaskFlags operator| ( EUnitTaskFlags Lhs, EUnitTaskFlags Rhs )

EMinClientFlags operator| ( EMinClientFlags Lhs, EMinClientFlags Rhs )

EUnitTestFlags operator| ( EUnitTestFlags Lhs, EUnitTestFlags Rhs )

ELogTraceFlags operator| ( ELogTraceFlags Lhs, ELogTraceFlags Rhs )

ELogType operator| ( ELogType Lhs, ELogType Rhs )

EUnitTaskFlags & operator|= ( EUnitTaskFlags& Lhs, EUnitTaskFlags Rhs )

EMinClientFlags & operator|= ( EMinClientFlags& Lhs, EMinClientFlags Rhs )

EUnitTestFlags & operator|= ( EUnitTestFlags& Lhs, EUnitTestFlags Rhs )

ELogTraceFlags & operator|= ( ELogTraceFlags& Lhs, ELogTraceFlags Rhs )

ELogType & operator|= ( ELogType& Lhs, ELogType Rhs )

EUnitTaskFlags operator~ ( EUnitTaskFlags E )

EMinClientFlags operator~ ( EMinClientFlags E )

EUnitTestFlags operator~ ( EUnitTestFlags E )

ELogTraceFlags operator~ ( ELogTraceFlags E )

ELogType operator~ ( ELogType E )

ELogType OptionalFlags ( ELogType InFlags )

EMinClientFlags ValidateMinFlags ( EMinClientFlags RuntimeFlags )



---

## NetworkPredictionExtrasLatentLoad

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NetworkPredictionExtrasLatentLoa-

**Contents:**
- NetworkPredictionExtrasLatentLoad
- Navigation
- Classes
- Interfaces



---

## NetworkPredictionExtras

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NetworkPredictionExtras

**Contents:**
- NetworkPredictionExtras
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables



---

## NetworkPredictionInsights

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NetworkPredictionInsights

**Contents:**
- NetworkPredictionInsights
- Navigation
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public
- Functions

uint64 FindMaxIndexPagedArray ( const TraceServices::TPagedArray< T >& PageArray, uint64 MaxFrameNumber )

int32 FindMaxIndexTArray ( const TArray< const T* >& Array, uint64 MaxFrameNumber, int32 StartIdx )

uint64 FindMinIndexPagedArray ( const TraceServices::TPagedArray< T >& PageArray, uint64 MinFrameNumber )

int32 FindMinIndexTArray ( const TArray< const T* >& Array, uint64 MinFrameNumber )

TEnableIf::Value, uint64 >::Type GetEngineFrame ( const T& Element )

TEnableIf< TIsPointer< T >::Value, uint64 >::Type GetEngineFrame ( const T& Element )

const TCHAR * LexToString ( ENP_NetRole Role )

const TCHAR * LexToString ( ENP_UserState State )

const TCHAR * LexToString ( ENP_UserStateSource Source )

const TCHAR * LexToString ( ENetSerializeRecvStatus Status )

const TCHAR * LexToString ( ENP_TickingPolicy Policy )

const INetworkPredictionProvider * ReadNetworkPredictionProvider ( const TraceServices::IAnalysisSession& Session )



---

## NetworkPrediction

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NetworkPrediction

**Contents:**
- NetworkPrediction
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

ENUM_CLASS_FLAGS ( ENetworkPredictionTickingPolicy )

ENUM_CLASS_FLAGS ( ENetworkLOD )

IConsoleVariable * FindConsoleVarHelper ( const TCHAR* VarName )

FString LexToString ( EReplicationProxyTarget A )

const TCHAR * LexToString ( ENetworkPredictionStateType A )

int32 NetworkPredictionCVars::DisableInterpolation()

int32 NetworkPredictionCVars::DisableSmoothing()

int32 NetworkPredictionCVars::DrawInterpolation()

int32 NetworkPredictionCVars::ForceReconcile()

int32 NetworkPredictionCVars::ForceReconcileExtraFrames()

int32 NetworkPredictionCVars::ForceSendDefaultInputCommands()

int32 NetworkPredictionCVars::PrintReconciles()

int32 NetworkPredictionCVars::PrintSyncInterpolation()

void NetworkPredictionCVars::SetDisableInterpolation ( int32 _V )

void NetworkPredictionCVars::SetDisableSmoothing ( int32 _V )

void NetworkPredictionCVars::SetDrawInterpolation ( int32 _V )

void NetworkPredictionCVars::SetForceReconcile ( int32 _V )

void NetworkPredictionCVars::SetForceReconcileExtraFrames ( int32 _V )

void NetworkPredictionCVars::SetForceSendDefaultInputCommands ( int32 _V )

void NetworkPredictionCVars::SetPrintReconciles ( int32 _V )

void NetworkPredictionCVars::SetPrintSyncInterpolation ( int32 _V )

void NetworkPredictionCVars::SetSkipReconcile ( int32 _V )

int32 NetworkPredictionCVars::SkipReconcile()

int32 NetworkPredictionPhysicsCvars::DebugPositionCorrections()

int32 NetworkPredictionPhysicsCvars::FullPrecision()

void NetworkPredictionPhysicsCvars::SetDebugPositionCorrections ( int32 _V )

void NetworkPredictionPhysicsCvars::SetFullPrecision ( int32 _V )

void NetworkPredictionPhysicsCvars::SetToleranceR ( float _V )

void NetworkPredictionPhysicsCvars::SetToleranceV ( float _V )

void NetworkPredictionPhysicsCvars::SetToleranceW ( float _V )

void NetworkPredictionPhysicsCvars::SetToleranceX ( float _V )

float NetworkPredictionPhysicsCvars::ToleranceR()

float NetworkPredictionPhysicsCvars::ToleranceV()

float NetworkPredictionPhysicsCvars::ToleranceW()

float NetworkPredictionPhysicsCvars::ToleranceX()

void NpClearBitArray ( BitArrayType& BitArray )

void NpResizeAndSetBit ( BitArrayType& BitArray, int32 Index, bool Value )

void NpResizeBitArray ( BitArrayType& BitArray, int32 NewNum )

void NpResizeForIndex ( ArrayType& Array, int32 Index )

bool operator! ( ESimulationTickContext E )

bool operator! ( ENetSimCueInvoker E )

bool operator! ( ENetSimCueReplicationTarget E )

bool operator! ( ENetworkPredictionService E )

ESimulationTickContext operator& ( ESimulationTickContext Lhs, ESimulationTickContext Rhs )

ENetSimCueInvoker operator& ( ENetSimCueInvoker Lhs, ENetSimCueInvoker Rhs )

ENetSimCueReplicationTarget operator& ( ENetSimCueReplicationTarget Lhs, ENetSimCueReplicationTarget Rhs )

ENetworkPredictionService operator& ( ENetworkPredictionService Lhs, ENetworkPredictionService Rhs )

ESimulationTickContext & operator&= ( ESimulationTickContext& Lhs, ESimulationTickContext Rhs )

ENetSimCueInvoker & operator&= ( ENetSimCueInvoker& Lhs, ENetSimCueInvoker Rhs )

ENetSimCueReplicationTarget & operator&= ( ENetSimCueReplicationTarget& Lhs, ENetSimCueReplicationTarget Rhs )

ENetworkPredictionService & operator&= ( ENetworkPredictionService& Lhs, ENetworkPredictionService Rhs )

ESimulationTickContext operator^ ( ESimulationTickContext Lhs, ESimulationTickContext Rhs )

ENetSimCueInvoker operator^ ( ENetSimCueInvoker Lhs, ENetSimCueInvoker Rhs )

ENetSimCueReplicationTarget operator^ ( ENetSimCueReplicationTarget Lhs, ENetSimCueReplicationTarget Rhs )

ENetworkPredictionService operator^ ( ENetworkPredictionService Lhs, ENetworkPredictionService Rhs )

ESimulationTickContext & operator^= ( ESimulationTickContext& Lhs, ESimulationTickContext Rhs )

ENetSimCueInvoker & operator^= ( ENetSimCueInvoker& Lhs, ENetSimCueInvoker Rhs )

ENetSimCueReplicationTarget & operator^= ( ENetSimCueReplicationTarget& Lhs, ENetSimCueReplicationTarget Rhs )

ENetworkPredictionService & operator^= ( ENetworkPredictionService& Lhs, ENetworkPredictionService Rhs )

ESimulationTickContext operator| ( ESimulationTickContext Lhs, ESimulationTickContext Rhs )

ENetSimCueInvoker operator| ( ENetSimCueInvoker Lhs, ENetSimCueInvoker Rhs )

ENetSimCueReplicationTarget operator| ( ENetSimCueReplicationTarget Lhs, ENetSimCueReplicationTarget Rhs )

ENetworkPredictionService operator| ( ENetworkPredictionService Lhs, ENetworkPredictionService Rhs )

ESimulationTickContext & operator|= ( ESimulationTickContext& Lhs, ESimulationTickContext Rhs )

ENetSimCueInvoker & operator|= ( ENetSimCueInvoker& Lhs, ENetSimCueInvoker Rhs )

ENetSimCueReplicationTarget & operator|= ( ENetSimCueReplicationTarget& Lhs, ENetSimCueReplicationTarget Rhs )

ENetworkPredictionService & operator|= ( ENetworkPredictionService& Lhs, ENetworkPredictionService Rhs )

ESimulationTickContext operator~ ( ESimulationTickContext E )

ENetSimCueInvoker operator~ ( ENetSimCueInvoker E )

ENetSimCueReplicationTarget operator~ ( ENetSimCueReplicationTarget E )

ENetworkPredictionService operator~ ( ENetworkPredictionService E )

int32 UE_NETWORK_PHYSICS::bFutureInputs()

int32 UE_NETWORK_PHYSICS::bInputDecay()

float UE_NETWORK_PHYSICS::DampYawVelocityK()

float UE_NETWORK_PHYSICS::DragK()

float UE_NETWORK_PHYSICS::InputDecayRate()

float UE_NETWORK_PHYSICS::JumpForce()

int32 UE_NETWORK_PHYSICS::JumpFrameDuration()

int32 UE_NETWORK_PHYSICS::JumpFudgeFrames()

int32 UE_NETWORK_PHYSICS::JumpHack()

int32 UE_NETWORK_PHYSICS::JumpMisPredict()

float UE_NETWORK_PHYSICS::MaxAngularVelocity()

int32 UE_NETWORK_PHYSICS::MockDebug()

int32 UE_NETWORK_PHYSICS::MockImpulse()

float UE_NETWORK_PHYSICS::MockImpulseX()

float UE_NETWORK_PHYSICS::MockImpulseZ()

float UE_NETWORK_PHYSICS::MovementK()

float UE_NETWORK_PHYSICS::RotationK()

void UE_NETWORK_PHYSICS::SetbFutureInputs ( int32 _V )

void UE_NETWORK_PHYSICS::SetbInputDecay ( int32 _V )

void UE_NETWORK_PHYSICS::SetDampYawVelocityK ( float _V )

void UE_NETWORK_PHYSICS::SetDragK ( float _V )

void UE_NETWORK_PHYSICS::SetInputDecayRate ( float _V )

void UE_NETWORK_PHYSICS::SetJumpForce ( float _V )

void UE_NETWORK_PHYSICS::SetJumpFrameDuration ( int32 _V )

void UE_NETWORK_PHYSICS::SetJumpFudgeFrames ( int32 _V )

void UE_NETWORK_PHYSICS::SetJumpHack ( int32 _V )

void UE_NETWORK_PHYSICS::SetJumpMisPredict ( int32 _V )

void UE_NETWORK_PHYSICS::SetMaxAngularVelocity ( float _V )

void UE_NETWORK_PHYSICS::SetMockDebug ( int32 _V )

void UE_NETWORK_PHYSICS::SetMockImpulse ( int32 _V )

void UE_NETWORK_PHYSICS::SetMockImpulseX ( float _V )

void UE_NETWORK_PHYSICS::SetMockImpulseZ ( float _V )

void UE_NETWORK_PHYSICS::SetMovementK ( float _V )

void UE_NETWORK_PHYSICS::SetRotationK ( float _V )

void UE_NETWORK_PHYSICS::SetTurnDampK ( float _V )

void UE_NETWORK_PHYSICS::SetTurnK ( float _V )

float UE_NETWORK_PHYSICS::TurnDampK()

float UE_NETWORK_PHYSICS::TurnK()

UE_TRACE_CHANNEL_EXTERN ( NetworkPredictionChannel )

static ENetworkLOD GetHighestNetworkLOD ( ENetworkLOD Mask )

static ESimulationTickContext GetSimTickMask ( const ENetSimCueInvoker Invoker, const bool bAllowResimulate )

static FConditionalAutoConsoleRegister NetworkPredictionCVars::ForceSendDefaultInputCommandsAuto ( TEXT("np.ForceSendDefaultInputCommands"), (int32) 0, TEXT("While enabled on a client, it will send default input cmds to the server, rather than the loca... )

static FConditionalAutoConsoleRegister NetworkPredictionPhysicsCvars::DebugPositionCorrectionsAuto ( TEXT("np.Physics.DebugPositionCorrections"), (int32) 0, TEXT("Prints position history when correcting physics X") )

static FConditionalAutoConsoleRegister NetworkPredictionPhysicsCvars::FullPrecisionAuto ( TEXT("np.Physics.FullPrecision"), (int32) 1, TEXT("Replicatre physics state with full precision. Not to be toggled during gameplay.") )

static FConditionalAutoConsoleRegister NetworkPredictionPhysicsCvars::ToleranceRAuto ( TEXT("np.Physics.Tolerance.R"), (float) 0. 1, TEXT("Normalized error tolerance between rotation (0..1)") )

static FConditionalAutoConsoleRegister NetworkPredictionPhysicsCvars::ToleranceVAuto ( TEXT("np.Physics.Tolerance.V"), (float) 1. 0, TEXT("Absolute error tolerance for velocity ") )

static FConditionalAutoConsoleRegister NetworkPredictionPhysicsCvars::ToleranceWAuto ( TEXT("np.Physics.Tolerance.W"), (float) 1. 0, TEXT("Absolute error tolerance for rotational velocity ") )

static FConditionalAutoConsoleRegister NetworkPredictionPhysicsCvars::ToleranceXAuto ( TEXT("np.Physics.Tolerance.X"), (float) 1. 0, TEXT("Absolute tolerance for position") )

static FConditionalAutoConsoleRegister UE_NETWORK_PHYSICS::bFutureInputsAuto ( TEXT("np2.FutureInputs"), (int32) 0, TEXT("Enable FutureInputs feature") )

static FConditionalAutoConsoleRegister UE_NETWORK_PHYSICS::bInputDecayAuto ( TEXT("np2.InputDecay"), (int32) 0, TEXT("Enable Input Decay Feature") )

static FConditionalAutoConsoleRegister UE_NETWORK_PHYSICS::DampYawVelocityKAuto ( TEXT("np2.Mock.DampYawVelocityK"), (float) 2. f, TEXT("Coefficient for damping angular velocity in yaw direction only. This is only enabled when auto... )

static FConditionalAutoConsoleRegister UE_NETWORK_PHYSICS::DragKAuto ( TEXT("np2.Mock.DragK"), (float) 1. 12f, TEXT("Drag Coefficient (higher=more drag)") )

static FConditionalAutoConsoleRegister UE_NETWORK_PHYSICS::InputDecayRateAuto ( TEXT("np2.InputDecayRate"), (float) 0. 99f, TEXT("Rate of input decay") )

static FConditionalAutoConsoleRegister UE_NETWORK_PHYSICS::JumpForceAuto ( TEXT("np2.Mock.JumpForce"), (float) 70, TEXT("Per-Frame force to apply while jumping.") )

static FConditionalAutoConsoleRegister UE_NETWORK_PHYSICS::JumpFrameDurationAuto ( TEXT("np2.Mock.JumpFrameDuration"), (int32) 4, TEXT("How many frames to apply jump force for") )

static FConditionalAutoConsoleRegister UE_NETWORK_PHYSICS::JumpFudgeFramesAuto ( TEXT("np2.Mock.JumpFudgeFrames"), (int32) 10, TEXT("How many frames after being in air do we still allow a jump to begin") )

static FConditionalAutoConsoleRegister UE_NETWORK_PHYSICS::JumpHackAuto ( TEXT("np2.Mock.JumpHack"), (int32) 0, TEXT("Make jump not rely on trace which currently causes non determinism") )

static FConditionalAutoConsoleRegister UE_NETWORK_PHYSICS::JumpMisPredictAuto ( TEXT("np2.Mock.JumpMisPredict"), (int32) 0, TEXT("Make jump do random impulse which will cause a misprediction") )

static FConditionalAutoConsoleRegister UE_NETWORK_PHYSICS::MaxAngularVelocityAuto ( TEXT("np2.Mock.MaxAngularVelocity"), (float) 30. f, TEXT("Limits how fast character can possibly rotate.") )

static FConditionalAutoConsoleRegister UE_NETWORK_PHYSICS::MockDebugAuto ( TEXT("np2.Mock.MockDebug"), (int32) 0, TEXT("Enabled spammy log debugging of mock physics object state") )

static FConditionalAutoConsoleRegister UE_NETWORK_PHYSICS::MockImpulseAuto ( TEXT("np2.Mock.BallImpulse"), (int32) 1, TEXT("Make jump not rely on trace which currently causes non determinism") )

static FConditionalAutoConsoleRegister UE_NETWORK_PHYSICS::MockImpulseXAuto ( TEXT("np2.Mock.BallImpulse.X"), (float) 500. 0f, TEXT("X magnitude") )

static FConditionalAutoConsoleRegister UE_NETWORK_PHYSICS::MockImpulseZAuto ( TEXT("np2.Mock.BallImpulse.Z"), (float) 300. 0f, TEXT("Z magnitude") )

static FConditionalAutoConsoleRegister UE_NETWORK_PHYSICS::MovementKAuto ( TEXT("np2.Mock.MovementK"), (float) 1. 25, TEXT("Movement Coefficient (higher=faster movement)") )

static FConditionalAutoConsoleRegister UE_NETWORK_PHYSICS::RotationKAuto ( TEXT("np2.Mock.RotationK"), (float) 1. 25, TEXT("Rotation Coefficient (higher=faster movement)") )

static FConditionalAutoConsoleRegister UE_NETWORK_PHYSICS::TurnDampKAuto ( TEXT("np2.Mock.TurnDampK"), (float) 100. f, TEXT("Coefficient for damping portion of turn. Higher=more damping but too higher will lead to insta... )

static FConditionalAutoConsoleRegister UE_NETWORK_PHYSICS::TurnKAuto ( TEXT("np2.Mock.TurnK"), (float) 100000000. f, TEXT("Coefficient for automatic turning (higher=quicker turning)") )



---

## NeuralMorphModelEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NeuralMorphModelEditor

**Contents:**
- NeuralMorphModelEditor
- Navigation
- Classes



---

## NeuralMorphModel

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NeuralMorphModel

**Contents:**
- NeuralMorphModel
- Navigation
- Classes
- Structs
- Enums
  - Public
- Variables
  - Public



---

## NeuralPostProcessing

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NeuralPostProcessing

**Contents:**
- NeuralPostProcessing
- Navigation
- Classes



---

## NFORDenoise

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NFORDenoise

**Contents:**
- NFORDenoise
- Navigation
- Classes



---

## NiagaraAnimNotifies

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NiagaraAnimNotifies

**Contents:**
- NiagaraAnimNotifies
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## NiagaraCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NiagaraCore

**Contents:**
- NiagaraCore
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

uint32 GetTypeHash ( const FNiagaraCompileHash& Hash )

bool operator!= ( const FSHAHash& Lhs, const FNiagaraCompileHash& Rhs )

bool operator== ( const FSHAHash& Lhs, const FNiagaraCompileHash& Rhs )



---

## NiagaraEditorWidgets

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NiagaraEditorWidgets

**Contents:**
- NiagaraEditorWidgets
- Navigation
- Classes



---

## NiagaraEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NiagaraEditor

**Contents:**
- NiagaraEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

FNiagaraVariableBase DecodeVariableAsSpecifiers ( UNiagaraNodeFunctionCall* Node )

void EncodeVariableAsSpecifiers ( const FNiagaraVariableBase& Var, UNiagaraNodeFunctionCall* TargetNode )

bool FNiagaraEditorUtilities::AddEmitterContextMenuActions ( FMenuBuilder& MenuBuilder, const TSharedPtr< FNiagaraEmitterHandleViewModel >& EmitterHandleViewModel )

const FGuid FNiagaraEditorUtilities::AddEmitterToSystem ( UNiagaraSystem& InSystem, UNiagaraEmitter& InEmitterToAdd, FGuid EmitterVersion, bool bCreateCopy )

bool FNiagaraEditorUtilities::AddParameter ( FNiagaraVariable& NewParameterVariable, FNiagaraParameterStore& TargetParameterStore, UObject& ParameterStoreOwner, UNiagaraStackEditorData* StackEditorData )

bool FNiagaraEditorUtilities::AreTypesAssignable ( const FNiagaraTypeDefinition& FromType, const FNiagaraTypeDefinition& ToType )

bool FNiagaraEditorUtilities::ArrayMatchesSet ( const TArray< ElementType >& Array, const TSet< ElementType >& Set )

void FNiagaraEditorUtilities::CompileExistingEmitters ( const TArray< FVersionedNiagaraEmitter >& AffectedEmitters )

void FNiagaraEditorUtilities::CopyDataTo ( FStructOnScope& DestinationStructOnScope, const FStructOnScope& SourceStructOnScope, bool bCheckTypes )

void FNiagaraEditorUtilities::CreateAssetFromEmitter ( TSharedRef< FNiagaraEmitterHandleViewModel > EmitterHandleViewModel )

TSharedPtr< SWidget > FNiagaraEditorUtilities::CreateInlineErrorText ( TAttribute< FText > ErrorMessage, TAttribute< FText > ErrorTooltip )

bool FNiagaraEditorUtilities::DataMatches ( const FNiagaraVariable& Variable, const FStructOnScope& StructOnScope )

bool FNiagaraEditorUtilities::DataMatches ( const FNiagaraVariable& VariableA, const FNiagaraVariable& VariableB )

bool FNiagaraEditorUtilities::DataMatches ( const FStructOnScope& StructOnScopeA, const FStructOnScope& StructOnScopeB )

TArray< FName > FNiagaraEditorUtilities::DecomposeVariableNamespace ( const FName& InVarNameToken, FName& OutName )

bool FNiagaraEditorUtilities::DoesItemMatchFilterText ( const FText& FilterText, const TSharedPtr< FNiagaraMenuAction_Generic >& Item )

TArray< UNiagaraParameterDefinitions * > FNiagaraEditorUtilities::DowncastParameterDefinitionsBaseArray ( const TArray< UNiagaraParameterDefinitionsBase* > BaseArray )

void FNiagaraEditorUtilities::FixUpNumericPins ( const UEdGraphSchema_Niagara* Schema, UNiagaraNode* Node )

void FNiagaraEditorUtilities::FixUpPastedNodes ( UEdGraph* Graph, TSet< UEdGraphNode* > PastedNodes )

FText FNiagaraEditorUtilities::FormatScriptDescription ( FText Description, const FSoftObjectPath& Path, bool bIsInLibrary )

FText FNiagaraEditorUtilities::FormatScriptName ( FName Name, bool bIsInLibrary )

FText FNiagaraEditorUtilities::FormatVariableDescription ( FText Description, FText Name, FText Type )

void FNiagaraEditorUtilities::GatherChangeIds ( UNiagaraEmitter& Emitter, TMap< FGuid, FGuid >& ChangeIds, const FString& InDebugName, bool bWriteToLogDir )

void FNiagaraEditorUtilities::GatherChangeIds ( UNiagaraGraph& Graph, TMap< FGuid, FGuid >& ChangeIds, const FString& InDebugName, bool bWriteToLogDir )

void FNiagaraEditorUtilities::GetAllowedEmitterVariableTypes ( TArray< FNiagaraTypeDefinition >& OutAllowedTypes )

void FNiagaraEditorUtilities::GetAllowedParameterTypes ( TArray< FNiagaraTypeDefinition >& OutAllowedTypes )

void FNiagaraEditorUtilities::GetAllowedParticleVariableTypes ( TArray< FNiagaraTypeDefinition >& OutAllowedTypes )

void FNiagaraEditorUtilities::GetAllowedPayloadTypes ( TArray< FNiagaraTypeDefinition >& OutAllowedTypes )

void FNiagaraEditorUtilities::GetAllowedSystemVariableTypes ( TArray< FNiagaraTypeDefinition >& OutAllowedTypes )

void FNiagaraEditorUtilities::GetAllowedUserVariableTypes ( TArray< FNiagaraTypeDefinition >& OutAllowedTypes )

TArray< UNiagaraParameterDefinitions * > FNiagaraEditorUtilities::GetAllParameterDefinitions ()

void FNiagaraEditorUtilities::GetAvailableParameterCollections ( TArray< UNiagaraParameterCollection* >& OutParameterCollections )

void FNiagaraEditorUtilities::GetAvailableParameterDefinitions ( TArray< UNiagaraParameterDefinitions* >& OutParameterDefinitions )

bool FNiagaraEditorUtilities::GetAvailableParameterDefinitions ( const TArray< FString >& ExternalPackagePaths, TArray< FAssetData >& OutParameterDefinitionsAssetData )

TArray< UNiagaraComponent * > FNiagaraEditorUtilities::GetComponentsThatReferenceSystem ( const UNiagaraSystem& ReferencedSystem )

TArray< UNiagaraComponent * > FNiagaraEditorUtilities::GetComponentsThatReferenceSystemViewModel ( const FNiagaraSystemViewModel& ReferencedSystemViewModel )

const FNiagaraEmitterHandle * FNiagaraEditorUtilities::GetEmitterHandleForEmitter ( UNiagaraSystem& System, const FVersionedNiagaraEmitter& Emitter )

void FNiagaraEditorUtilities::GetFilteredScriptAssets ( FGetFilteredScriptAssetsOptions InFilter, TArray< FAssetData >& OutFilteredScriptAssets )

bool FNiagaraEditorUtilities::GetIsInheritableFromAssetRegistryTags ( const FAssetData& AssetData, bool& bUseInheritance )

const FGuid & FNiagaraEditorUtilities::GetNamespaceIdForUsage ( ENiagaraScriptUsage Usage )

FString FNiagaraEditorUtilities::GetNamespacelessVariableNameString ( const FName& InVarName )

const FNiagaraNamespaceMetadata FNiagaraEditorUtilities::GetNamespaceMetaDataForId ( const FGuid& NamespaceId )

const FNiagaraNamespaceMetadata FNiagaraEditorUtilities::GetNamespaceMetaDataForVariableName ( const FName& VarName )

int32 FNiagaraEditorUtilities::GetNamespaceMetaDataSortPriority ( const FNiagaraNamespaceMetadata& A, const FNiagaraNamespaceMetadata& B )

int32 FNiagaraEditorUtilities::GetNamespaceSortPriority ( const FName& Namespace )

TSharedPtr< INiagaraParameterDefinitionsSubscriberViewModel > FNiagaraEditorUtilities::GetOwningLibrarySubscriberViewModelForGraph ( const UNiagaraGraph* Graph )

void FNiagaraEditorUtilities::GetParameterVariablesFromSystem ( UNiagaraSystem& System, TArray< FNiagaraVariable >& ParameterVariables, FGetParameterVariablesFromSystemOptions Options )

int FNiagaraEditorUtilities::GetReferencedAssetCount ( const FAssetData& SourceAsset, TFunction< ETrackAssetResult(const FAssetData&)> Predicate )

void FNiagaraEditorUtilities::GetReferencingFunctionCallNodes ( UNiagaraScript* Script, TArray< UNiagaraNodeFunctionCall* >& OutReferencingFunctionCallNodes )

UNiagaraDataInterface * FNiagaraEditorUtilities::GetResolvedRuntimeInstanceForEditorDataInterfaceInstance ( const UNiagaraSystem& OwningSystem, UNiagaraDataInterface& EditorDataInterfaceInstance )

float FNiagaraEditorUtilities::GetScalabilityTintAlpha ( FNiagaraEmitterHandle* EmitterHandle )

ENiagaraScriptLibraryVisibility FNiagaraEditorUtilities::GetScriptAssetVisibility ( const FAssetData& ScriptAssetData )

UNiagaraScript * FNiagaraEditorUtilities::GetScriptFromSystem ( UNiagaraSystem& System, FGuid EmitterHandleId, ENiagaraScriptUsage Usage, FGuid UsageId )

void FNiagaraEditorUtilities::GetScriptMessageStores ( UNiagaraScript* InScript, TArray< FNiagaraMessageSourceAndStore >& OutNiagaraMessageStores )

UNiagaraNodeOutput * FNiagaraEditorUtilities::GetScriptOutputNode ( UNiagaraScript& Script )

TTuple< EScriptSource, FText > FNiagaraEditorUtilities::GetScriptSource ( const FAssetData& ScriptAssetData )

FLinearColor FNiagaraEditorUtilities::GetScriptSourceColor ( EScriptSource ScriptSourceData )

ECheckBoxState FNiagaraEditorUtilities::GetSelectedEmittersEnabledCheckState ( TSharedRef< FNiagaraSystemViewModel > SystemViewModel )

ECheckBoxState FNiagaraEditorUtilities::GetSelectedEmittersIsolatedCheckState ( TSharedRef< FNiagaraSystemViewModel > SystemViewModel )

TSet< FName > FNiagaraEditorUtilities::GetSystemConstantNames()

bool FNiagaraEditorUtilities::GetTemplateSpecificationFromTag ( const FAssetData& Data, ENiagaraScriptTemplateSpecification& OutTemplateSpecification )

void FNiagaraEditorUtilities::GetTypeDefaultValue ( const FNiagaraTypeDefinition& Type, TArray< uint8 >& DefaultData )

FText FNiagaraEditorUtilities::GetTypeDefinitionCategory ( const FNiagaraTypeDefinition& TypeDefinition )

FName FNiagaraEditorUtilities::GetUniqueObjectName ( UObject* Outer, const FString& CandidateName )

FName FNiagaraEditorUtilities::GetUniqueObjectName ( UObject* Outer, UClass* ObjectClass, const FString& CandidateName )

TArray< FVariableAttributeBindingInfo > FNiagaraEditorUtilities::GetVariableAttributeBindingsForParameter ( TSharedRef< FNiagaraSystemViewModel > SystemViewModel, FNiagaraVariable Parameter, const FNiagaraActionScopeConfig& Config )

bool FNiagaraEditorUtilities::GetVariableSortPriority ( const FName& VarNameA, const FName& VarNameB )

FText FNiagaraEditorUtilities::GetVariableTypeCategory ( const FNiagaraVariable& Variable )

int32 FNiagaraEditorUtilities::GetWeightForItem ( const TSharedPtr< FNiagaraMenuAction_Generic >& Item, FName FavoriteActionsProfile, const TArray< FString >& FilterTerms )

TSharedRef< SWidget > FNiagaraEditorUtilities::HierarchyEditor::Scripts::GenerateRowContentForScriptParameterHierarchyEditor ( TSharedRef< FHierarchyElementViewModel > HierarchyItem )

void FNiagaraEditorUtilities::InfoWithToastAndLog ( FText WarningMessage, float ToastDuration )

void FNiagaraEditorUtilities::InitializeParameterInputNode ( UNiagaraNodeInput& InputNode, const FNiagaraTypeDefinition& Type, const UNiagaraGraph* Graph, FName InputName )

bool FNiagaraEditorUtilities::IsClassVisibileInGlobalFilter ( UClass* Class )

bool FNiagaraEditorUtilities::IsCompilableAssetClass ( UClass* AssetClass )

bool FNiagaraEditorUtilities::IsEditorDataInterfaceInstance ( const UNiagaraDataInterface* DataInterface )

bool FNiagaraEditorUtilities::IsEnginePluginAsset ( const FTopLevelAssetPath& InTopLevelAssetPath )

bool FNiagaraEditorUtilities::IsEnumIndexVisible ( const UEnum* Enum, int32 Index )

bool FNiagaraEditorUtilities::IsScriptAssetInLibrary ( const FAssetData& ScriptAssetData )

void FNiagaraEditorUtilities::KillSystemInstances ( const UNiagaraSystem& System )

void FNiagaraEditorUtilities::MarkDependentCompilableAssetsDirty ( TArray< UObject* > InObjects )

void FNiagaraEditorUtilities::MarkDependentCompilableAssetsDirty ( const TArray< FAssetData >& InAssets )

bool FNiagaraEditorUtilities::NestedPropertiesAppendCompileHash ( const void* Container, const UStruct* Struct, EFieldIteratorFlags::SuperClassFlags IteratorFlags, FStringView BaseName, FNiagaraCompileHashVisitor* InVisitor )

void FNiagaraEditorUtilities::OpenParentEmitterForEdit ( TSharedRef< FNiagaraEmitterViewModel > Emitter )

bool FNiagaraEditorUtilities::PODPropertyAppendCompileHash ( const void* Container, FProperty* Property, FStringView PropertyName, FNiagaraCompileHashVisitor* InVisitor )

void FNiagaraEditorUtilities::PreprocessFunctionGraph ( const UEdGraphSchema_Niagara* Schema, UNiagaraGraph* Graph, TArrayView< UEdGraphPin*const > CallInputs, TArrayView< UEdGraphPin*const > CallOutputs, ENiagaraScriptUsage ScriptUsage, const FCompileConstantResolver& ConstantResolver )

TOptional< FSoftObjectPath > FNiagaraEditorUtilities::Preview::GetPreviewMovieObjectPath ( const FAssetData& AssetData )

void FNiagaraEditorUtilities::RecomposeVariableNamespace ( const FName& InVarNameToken, const TArray< FName >& InParentNamespaces, FName& OutName )

void FNiagaraEditorUtilities::RefreshAllScriptsFromExternalChanges ( FRefreshAllScriptsFromExternalChangesArgs Args )

void FNiagaraEditorUtilities::RemoveEmittersFromSystemByEmitterHandleId ( UNiagaraSystem& InSystem, TSet< FGuid > EmitterHandleIdsToDelete )

void FNiagaraEditorUtilities::ResetSystemsThatReferenceSystemViewModel ( const FNiagaraSystemViewModel& ReferencedSystemViewModel )

void FNiagaraEditorUtilities::ResetVariableToDefaultValue ( FNiagaraVariable& Variable )

bool FNiagaraEditorUtilities::ResolveConstantValue ( UEdGraphPin* Pin, int32& Value )

void FNiagaraEditorUtilities::ResolveNumerics ( UNiagaraGraph* SourceGraph, bool bForceParametersToResolveNumerics, TArray< FNiagaraVariable >& ChangedNumericParams )

UNiagaraClipboardContent * FNiagaraEditorUtilities::RunPythonConversionScript ( FVersionedNiagaraScriptData& NewScriptVersionData, UNiagaraClipboardContent* NewScriptInputs, FVersionedNiagaraScriptData& OldScriptVersionData, UNiagaraClipboardContent* OldScriptInputs, FText& OutWarnings )

void FNiagaraEditorUtilities::RunPythonUpgradeScripts ( UUpgradeNiagaraEmitterContext* UpgradeContext )

void FNiagaraEditorUtilities::RunPythonUpgradeScripts ( UNiagaraNodeFunctionCall* SourceNode, const TArray< FVersionedNiagaraScriptData* >& UpgradeVersionData, const FNiagaraScriptVersionUpgradeContext& UpgradeContext, FString& OutWarnings )

TMap< FNiagaraVariableBase, FGuid > FNiagaraEditorUtilities::Scripts::Validation::FixupDuplicateScriptVariableGuids ( UNiagaraScript* Script )

TMap< FGuid, TArray< FNiagaraVariableBase > > FNiagaraEditorUtilities::Scripts::Validation::ValidateScriptVariableIds ( UNiagaraScript* Script, FGuid VersionGuid )

bool FNiagaraEditorUtilities::SetsMatch ( const TSet< ElementType >& SetA, const TSet< ElementType >& SetB )

void FNiagaraEditorUtilities::SetStaticSwitchConstants ( UNiagaraGraph* Graph, TArrayView< UEdGraphPin*const > CallInputs, const FCompileConstantResolver& ConstantResolver )

void FNiagaraEditorUtilities::ShowParentEmitterInContentBrowser ( TSharedRef< FNiagaraEmitterViewModel > EmitterViewModel )

TSharedPtr< FStructOnScope > FNiagaraEditorUtilities::StaticSwitchDefaultIntToStructOnScope ( int32 InStaticSwitchDefaultValue, FNiagaraTypeDefinition InSwitchType )

FText FNiagaraEditorUtilities::StatusToText ( ENiagaraScriptCompileStatus Status )

void FNiagaraEditorUtilities::SwitchParentEmitterVersion ( TSharedRef< FNiagaraEmitterViewModel > EmitterViewModel, TSharedRef< FNiagaraSystemViewModel > SystemViewModel, const FGuid& NewVersionGuid )

void FNiagaraEditorUtilities::ToggleSelectedEmittersEnabled ( TSharedRef< FNiagaraSystemViewModel > SystemViewModel )

void FNiagaraEditorUtilities::ToggleSelectedEmittersIsolated ( TSharedRef< FNiagaraSystemViewModel > SystemViewModel )

TSharedRef< SToolTip > FNiagaraEditorUtilities::Tooltips::CreateStackNoteTooltip ( UNiagaraStackNote& StackNote )

TSharedRef< SToolTip > FNiagaraEditorUtilities::Tooltips::CreateTooltip ( FText Description, TOptional< FSoftObjectPath > PreviewMoviePath, const FCreateTooltipArguments& CreateTooltipArguments )

TSharedRef< SToolTip > FNiagaraEditorUtilities::Tooltips::CreateTooltipForNiagaraAction ( TSharedRef< FNiagaraMenuAction_Generic > Action, const FCreateTooltipArguments& CreateTooltipArguments )

TSharedRef< SToolTip > FNiagaraEditorUtilities::Tooltips::CreateTooltipForScript ( UNiagaraScript& Script, FGuid VersionGuid, const FCreateTooltipArguments& CreateTooltipArguments )

FText FNiagaraEditorUtilities::Tooltips::GetMinimalEmitterCreationTooltip()

bool FNiagaraEditorUtilities::TryGetEventDisplayName ( UNiagaraEmitter* Emitter, FGuid EventUsageId, FText& OutEventDisplayName )

ENiagaraScriptCompileStatus FNiagaraEditorUtilities::UnionCompileStatus ( const ENiagaraScriptCompileStatus& StatusA, const ENiagaraScriptCompileStatus& StatusB )

void FNiagaraEditorUtilities::UserParameters::DeleteUserParameterReferences ( TSharedRef< FNiagaraSystemViewModel > SystemViewModel, FNiagaraVariable UserParameterToDelete, const FNiagaraActionScopeConfig& Config )

FNiagaraVariable FNiagaraEditorUtilities::UserParameters::DuplicateUserParameter ( FNiagaraVariable ParameterToDuplicate, UNiagaraSystem& System )

const UNiagaraScriptVariable * FNiagaraEditorUtilities::UserParameters::FindScriptVariableForUserParameter ( const FGuid& UserParameterGuid, const UNiagaraSystem& System )

TArray< UNiagaraNodeParameterMapGet * > FNiagaraEditorUtilities::UserParameters::GetParameterMapGetNodesWithUserParameter ( TSharedRef< FNiagaraSystemViewModel > SystemViewModel, FNiagaraVariable UserParameter, const FNiagaraActionScopeConfig& Config )

TArray< FNiagaraVariable > FNiagaraEditorUtilities::UserParameters::GetReferencedUserParametersFromEmitter ( TSharedRef< FNiagaraEmitterViewModel > EmitterViewModel )

TObjectPtr< UNiagaraScriptVariable > FNiagaraEditorUtilities::UserParameters::GetScriptVariableForUserParameter ( const FNiagaraVariable& UserParameter, TSharedPtr< FNiagaraSystemViewModel > SystemViewModel )

TObjectPtr< UNiagaraScriptVariable > FNiagaraEditorUtilities::UserParameters::GetScriptVariableForUserParameter ( const FNiagaraVariable& UserParameter, UNiagaraSystem& System )

TArray< UNiagaraStackFunctionInput * > FNiagaraEditorUtilities::UserParameters::GetStackFunctionInputsWithLinkedParameter ( TSharedRef< FNiagaraSystemViewModel > SystemViewModel, FNiagaraVariable Parameter, const FNiagaraActionScopeConfig& Config )

TArray< FUserParameterBindingInfo > FNiagaraEditorUtilities::UserParameters::GetUserParameterBindingsForUserParameter ( TSharedRef< FNiagaraSystemViewModel > SystemViewModel, FNiagaraVariable UserParameter, const FNiagaraActionScopeConfig& Config )

void FNiagaraEditorUtilities::UserParameters::ReplaceUserParameterReferences ( TSharedRef< FNiagaraSystemViewModel > SystemViewModel, FNiagaraVariable OldUserParameter, FNiagaraVariable NewUserParameter, const FNiagaraActionScopeConfig& Config )

EAxisList::Type FNiagaraEditorUtilities::VectorComponentToAxis ( int32 NumComponents, int32 ComponentIndex )

bool FNiagaraEditorUtilities::VerifyNameChangeForInputOrOutputNode ( const UNiagaraNode& NodeBeingChanged, FName OldName, FString NewName, FText& OutErrorMessage )

void FNiagaraEditorUtilities::VisitAllNodesConnectedToInputs ( UEdGraphNode* StartNode, FNodeVisitor Visitor )

void FNiagaraEditorUtilities::WarnWithToastAndLog ( FText WarningMessage )

void FNiagaraEditorUtilities::WriteTextFileToDisk ( FString SaveDirectory, FString FileName, FString TextToSave, bool bAllowOverwriting )

FText FNiagaraMessageUtilities::GetShortDescriptionFromSeverity ( EStackIssueSeverity Severity )

FText FNiagaraMessageUtilities::MakePostCompileSummaryText ( const FText& CompileObjectNameText, ENiagaraScriptCompileStatus LatestCompileStatus, const int32& WarningCount, const int32& ErrorCount )

UNiagaraStackEntry::FStackIssue FNiagaraMessageUtilities::MessageToStackIssue ( TSharedRef< const INiagaraMessage > InMessage, FString InStackEditorDataKey )

UNiagaraStackEntry::FStackIssue FNiagaraMessageUtilities::StackMessageToStackIssue ( const FNiagaraStackMessage& InMessage, FString InStackEditorDataKey, const TArray< FLinkNameAndDelegate >& InLinks )

TArray< const UNiagaraScriptVariable * > FNiagaraParameterDefinitionsUtilities::FindReservedParametersByName ( const FName ParameterName )

EParameterDefinitionMatchState FNiagaraParameterDefinitionsUtilities::GetDefinitionMatchStateForParameter ( const FNiagaraVariableBase& Parameter )

int32 FNiagaraParameterDefinitionsUtilities::GetNumParametersReservedForName ( const FName ParameterName )

void FNiagaraParameterDefinitionsUtilities::TrySubscribeScriptVarToDefinitionByName ( UNiagaraScriptVariable* ScriptVar, INiagaraParameterDefinitionsSubscriberViewModel* OwningDefinitionSubscriberViewModel )

bool FNiagaraParameterPanelUtilities::GetCanSetParameterCustomNamespaceModifierAndToolTipForScriptOrSystem ( const FNiagaraParameterPanelItem& ItemToModify, bool bDuplicateParameter, FText& OutCanSetParameterNamespaceModifierToolTip )

bool FNiagaraParameterPanelUtilities::GetCanSetParameterNamespaceAndToolTipForScriptOrSystem ( const FNiagaraParameterPanelItem& ItemToModify, const FName NewNamespace, FText& OutCanSetParameterNamespaceToolTip )

bool FNiagaraParameterPanelUtilities::GetCanSetParameterNamespaceModifierAndToolTipForScriptOrSystem ( const TArray< FNiagaraParameterPanelItem >& CachedViewedItems, const FNiagaraParameterPanelItem& ItemToModify, const FName NamespaceModifier, bool bDuplicateParameter, FText& OutCanSetParameterNamespaceModifierToolTip )

FNiagaraVariable FNiagaraParameterUtilities::BasicAttributeToNamespacedAttribute ( const FNiagaraVariable& InVar, bool bSanitizeInput )

FName FNiagaraParameterUtilities::ChangeNamespace ( FName ParameterName, const FNiagaraNamespaceMetadata& NewNamespaceMetadata )

FNiagaraVariable FNiagaraParameterUtilities::ConvertVariableToRapidIterationConstantName ( FNiagaraVariable InVar, const TCHAR* InEmitterName, ENiagaraScriptUsage InUsage )

TSharedRef< SWidget > FNiagaraParameterUtilities::CreateNamespaceMenuItemWidget ( FName Namespace, FText ToolTip )

bool FNiagaraParameterUtilities::DoesParameterNameMatchSearchText ( FName ParameterName, const FString& SearchTextString )

void FNiagaraParameterUtilities::FilterToRelevantStaticVariables ( TConstArrayView< FNiagaraVariable > InVars, TArray< FNiagaraVariable >& OutVars, FName InOldEmitterAlias, FName InNewEmitterAlias, bool bFilterByEmitterAliasAndConvertToUnaliased )

FText FNiagaraParameterUtilities::FormatParameterNameForTextDisplay ( FName ParameterName )

void FNiagaraParameterUtilities::GetChangeNamespaceMenuData ( FName InParameterName, EParameterContext InParameterContext, TArray< FChangeNamespaceMenuData >& OutChangeNamespaceMenuData )

FName FNiagaraParameterUtilities::GetEditableNamespaceModifierForParameter ( FName ParameterName )

FString FNiagaraParameterUtilities::GetNamespace ( const FNiagaraVariable& InVar, bool bIncludeDelimiter )

bool FNiagaraParameterUtilities::GetNamespaceEditData ( FName InParameterName, FNiagaraParameterHandle& OutParameterHandle, FNiagaraNamespaceMetadata& OutNamespaceMetadata, FText& OutErrorMessage )

bool FNiagaraParameterUtilities::GetNamespaceModifierEditData ( FName InParameterName, FNiagaraParameterHandle& OutParameterHandle, FNiagaraNamespaceMetadata& OutNamespaceMetadata, FText& OutErrorMessage )

int32 FNiagaraParameterUtilities::GetNumberOfNamePartsBeforeEditableModifier ( const FNiagaraNamespaceMetadata& NamespaceMetadata )

void FNiagaraParameterUtilities::GetOptionalNamespaceModifiers ( FName ParameterName, EParameterContext InParameterContext, TArray< FName >& OutOptionalNamespaceModifiers )

TSharedRef< SWidget > FNiagaraParameterUtilities::GetParameterWidget ( FNiagaraVariable Variable, bool bAddTypeIcon, bool bShowValue )

TSharedRef< SWidget > FNiagaraParameterUtilities::GetParameterWidget ( FNiagaraVariable Variable, FNiagaraVariableMetaData MetaData, FNiagaraParameterWidgetOptions Options )

FNiagaraVariable FNiagaraParameterUtilities::GetSourceForInitialValue ( const FNiagaraVariable& InVar )

FName FNiagaraParameterUtilities::GetSourceForInitialValue ( const FName& InVariableName )

FNiagaraVariable FNiagaraParameterUtilities::GetSourceForPreviousValue ( const FNiagaraVariable& InVar )

FName FNiagaraParameterUtilities::GetSourceForPreviousValue ( const FName& InVariableName )

TSharedRef< SToolTip > FNiagaraParameterUtilities::GetTooltipWidget ( FNiagaraVariable Variable, bool bShowValue, TSharedPtr< SWidget > AdditionalVerticalWidget )

void FNiagaraParameterUtilities::GetValidNamespacesForReading ( const UNiagaraScript* InScript, TArray< FString >& OutputNamespaces )

void FNiagaraParameterUtilities::GetValidNamespacesForReading ( ENiagaraScriptUsage InScriptUsage, int32 InUsageBitmask, TArray< FString >& OutputNamespaces )

bool FNiagaraParameterUtilities::IsAliasedEmitterParameter ( const FNiagaraVariable& InVar )

bool FNiagaraParameterUtilities::IsAliasedEmitterParameter ( const FString& InVarName )

bool FNiagaraParameterUtilities::IsAliasedModuleParameter ( const FNiagaraVariable& InVar )

bool FNiagaraParameterUtilities::IsAttribute ( const FNiagaraVariableBase& InVar )

bool FNiagaraParameterUtilities::IsEngineParameter ( const FNiagaraVariable& InVar )

bool FNiagaraParameterUtilities::IsExportableExternalConstant ( const FNiagaraVariable& InVar, const UNiagaraScript* InScript )

bool FNiagaraParameterUtilities::IsExternalConstantNamespace ( const FNiagaraVariable& InVar, const UNiagaraScript* InScript, const FGuid& VersionGuid )

bool FNiagaraParameterUtilities::IsExternalConstantNamespace ( const FNiagaraVariable& InVar, ENiagaraScriptUsage InUsage, int32 InUsageBitmask )

bool FNiagaraParameterUtilities::IsInitialName ( const FName& InVariableName )

bool FNiagaraParameterUtilities::IsInitialValue ( const FNiagaraVariableBase& InVar )

bool FNiagaraParameterUtilities::IsInNamespace ( const FNiagaraVariableBase& InVar, const FString& Namespace )

bool FNiagaraParameterUtilities::IsPerInstanceEngineParameter ( const FNiagaraVariable& InVar, const FString& EmitterAlias )

bool FNiagaraParameterUtilities::IsPreviousName ( const FName& InVariableName )

bool FNiagaraParameterUtilities::IsPreviousValue ( const FNiagaraVariableBase& InVar )

bool FNiagaraParameterUtilities::IsRapidIterationParameter ( const FNiagaraVariable& InVar )

bool FNiagaraParameterUtilities::IsSystemParameter ( const FNiagaraVariable& InVar )

bool FNiagaraParameterUtilities::IsUserParameter ( const FNiagaraVariable& InVar )

bool FNiagaraParameterUtilities::IsValidNamespaceForReading ( ENiagaraScriptUsage InScriptUsage, int32 InUsageBitmask, FString Namespace )

bool FNiagaraParameterUtilities::IsWrittenToScriptUsage ( const FNiagaraVariable& InVar, ENiagaraScriptUsage InUsage, bool bAllowDataInterfaces )

FString FNiagaraParameterUtilities::MakeSafeNamespaceString ( const FString& InStr )

FNiagaraVariable FNiagaraParameterUtilities::MoveToExternalConstantNamespaceVariable ( const FNiagaraVariable& InVar, const UNiagaraScript* InScript )

FNiagaraVariable FNiagaraParameterUtilities::MoveToExternalConstantNamespaceVariable ( const FNiagaraVariable& InVar, ENiagaraScriptUsage InUsage )

FNiagaraVariable FNiagaraParameterUtilities::ResolveAsBasicAttribute ( const FNiagaraVariable& InVar, bool bSanitizeInput )

FName FNiagaraParameterUtilities::ResolveEmitterAlias ( const FName& InName, const FString& InAlias )

FName FNiagaraParameterUtilities::SetCustomNamespaceModifier ( FName InParameterName )

FName FNiagaraParameterUtilities::SetCustomNamespaceModifier ( FName InParameterName, TSet< FName >& CurrentParameterNames )

FName FNiagaraParameterUtilities::SetSpecificNamespaceModifier ( FName InParameterName, FName InNamespaceModifier )

bool FNiagaraParameterUtilities::SplitRapidIterationParameterName ( const FNiagaraVariable& InVar, ENiagaraScriptUsage InUsage, FString& EmitterName, FString& FunctionCallName, FString& InputName )

bool FNiagaraParameterUtilities::TestCanChangeNamespaceWithMessage ( FName ParameterName, const FNiagaraNamespaceMetadata& NewNamespaceMetadata, FText& OutMessage )

bool FNiagaraParameterUtilities::TestCanRenameWithMessage ( FName ParameterName, FText& OutMessage )

bool FNiagaraParameterUtilities::TestCanSetCustomNamespaceModifierWithMessage ( FName InParameterName, FText& OutMessage )

bool FNiagaraParameterUtilities::TestCanSetSpecificNamespaceModifierWithMessage ( FName InParameterName, FName InNamespaceModifier, FText& OutMessage )

FNiagaraVariable FNiagaraParameterUtilities::VariableToNamespacedVariable ( const FNiagaraVariable& InVar, FString Namespace )

FReply FNiagaraScriptToolkitParameterPanelUtilities::CreateDragEventForParameterItem ( const FNiagaraParameterPanelItemBase& DraggedItem, const FPointerEvent& MouseEvent, const TArray< FNiagaraGraphParameterReference >& GraphParameterReferencesForItem, const TSharedPtr< TArray< FName > >& ParametersWithNamespaceModifierRenamePending )

void FNiagaraStackClipboardUtilities::CopyNote ( const UNiagaraStackEntry* StackEntry )

void FNiagaraStackClipboardUtilities::CopySelection ( const TArray< UNiagaraStackEntry* >& SelectedEntries )

void FNiagaraStackClipboardUtilities::CutSelection ( const TArray< UNiagaraStackEntry* >& SelectedEntries )

void FNiagaraStackClipboardUtilities::DeleteSelection ( const TArray< UNiagaraStackEntry* >& SelectedEntries )

void FNiagaraStackClipboardUtilities::PasteSelection ( const TArray< UNiagaraStackEntry* >& SelectedEntries, FText& OutPasteWarning )

bool FNiagaraStackClipboardUtilities::TestCanCopySelectionWithMessage ( const TArray< UNiagaraStackEntry* >& SelectedEntries, FText& OutCanCopyMessage )

bool FNiagaraStackClipboardUtilities::TestCanCutSelectionWithMessage ( const TArray< UNiagaraStackEntry* >& SelectedEntries, FText& OutCanCutMessage )

bool FNiagaraStackClipboardUtilities::TestCanDeleteSelectionWithMessage ( const TArray< UNiagaraStackEntry* >& SelectedEntries, FText& OutMessage )

bool FNiagaraStackClipboardUtilities::TestCanPasteSelectionWithMessage ( const TArray< UNiagaraStackEntry* >& SelectedEntries, FText& OutCanPasteMessage )

void FNiagaraStackGraphUtilities::AddNewVariableToParameterMapNode ( UNiagaraNodeParameterMapBase* MapBaseNode, bool bCreateInputPin, const FNiagaraVariable& NewVariable )

void FNiagaraStackGraphUtilities::AddNewVariableToParameterMapNode ( UNiagaraNodeParameterMapBase* MapBaseNode, bool bCreateInputPin, const UNiagaraScriptVariable* NewScriptVar )

UNiagaraNodeAssignment * FNiagaraStackGraphUtilities::AddParameterModuleToStack ( const TArray< FNiagaraVariable >& ParameterVariables, UNiagaraNodeOutput& TargetOutputNode, int32 TargetIndex, const TArray< FString >& InDefaultValues )

UNiagaraNodeFunctionCall * FNiagaraStackGraphUtilities::AddScriptModuleToStack ( const FAddScriptModuleToStackArgs& Args )

UNiagaraNodeFunctionCall * FNiagaraStackGraphUtilities::AddScriptModuleToStack ( FAssetData ModuleScriptAsset, UNiagaraNodeOutput& TargetOutputNode, int32 TargetIndex, FString SuggestedName )

UNiagaraNodeFunctionCall * FNiagaraStackGraphUtilities::AddScriptModuleToStack ( UNiagaraScript* ModuleScript, UNiagaraNodeOutput& TargetOutputNode, int32 TargetIndex, FString SuggestedName, const FGuid& VersionGuid )

void FNiagaraStackGraphUtilities::BreakAllPinLinks ( UEdGraphPin* PinA )

void FNiagaraStackGraphUtilities::BuildParameterMapHistoryWithStackContextResolution ( FVersionedNiagaraEmitter OwningEmitter, UNiagaraNodeOutput* OutputNodeInChain, UNiagaraNode* NodeToVisit, TArray< FNiagaraParameterMapHistory >& OutHistories, bool bRecursive, bool bFilterForCompilation )

bool FNiagaraStackGraphUtilities::CanWriteParameterFromUsage ( FNiagaraVariable Parameter, ENiagaraScriptUsage Usage, const TOptional< FName >& StackContextOverride, const TArray< FName >& StackContextAllOverrides )

bool FNiagaraStackGraphUtilities::CanWriteParameterFromUsageViaOutput ( FNiagaraVariable Parameter, const UNiagaraNodeOutput* OutputNode )

void FNiagaraStackGraphUtilities::CheckForDeprecatedEmitterVersion ( TSharedPtr< FNiagaraEmitterViewModel > ViewModel, const FString& StackEditorDataKey, UNiagaraStackEntry::FStackIssueFixDelegate VersionUpgradeFix, TArray< UNiagaraStackEntry::FStackIssue >& OutIssues )

void FNiagaraStackGraphUtilities::CheckForDeprecatedScriptVersion ( UNiagaraNodeFunctionCall* InputFunctionCallNode, const FString& StackEditorDataKey, UNiagaraStackEntry::FStackIssueFixDelegate VersionUpgradeFix, TArray< UNiagaraStackEntry::FStackIssue >& OutIssues )

void FNiagaraStackGraphUtilities::CleanUpStaleRapidIterationParameters ( FVersionedNiagaraEmitter Emitter )

void FNiagaraStackGraphUtilities::CleanUpStaleRapidIterationParameters ( UNiagaraScript& Script, FVersionedNiagaraEmitter OwningEmitter )

void FNiagaraStackGraphUtilities::ConnectPinToInputNode ( UEdGraphPin& Pin, UNiagaraNodeInput& InputNode )

void FNiagaraStackGraphUtilities::ConnectStackNodeGroup ( const FStackNodeGroup& ConnectGroup, const FStackNodeGroup& NewPreviousGroup, const FStackNodeGroup& NewNextGroup )

FNiagaraVariable FNiagaraStackGraphUtilities::CreateRapidIterationParameter ( const FString& UniqueEmitterName, ENiagaraScriptUsage ScriptUsage, const FName& AliasedInputName, const FNiagaraTypeDefinition& InputType )

bool FNiagaraStackGraphUtilities::DependencyUtilities::DoesStackModuleProvideDependency ( const FNiagaraStackModuleData& StackModuleData, const FNiagaraModuleDependency& SourceModuleRequiredDependency, const UNiagaraNodeOutput& SourceOutputNode )

int32 FNiagaraStackGraphUtilities::DependencyUtilities::FindBestIndexForModuleInStack ( UNiagaraNodeFunctionCall& ModuleNode, const UNiagaraNodeOutput& TargetOutputNode )

void FNiagaraStackGraphUtilities::DependencyUtilities::GetModuleScriptAssetsByDependencyProvided ( FName DependencyName, TOptional< ENiagaraScriptUsage > RequiredUsage, TArray< FAssetData >& OutAssets )

void FNiagaraStackGraphUtilities::DisconnectStackNodeGroup ( const FStackNodeGroup& DisconnectGroup, const FStackNodeGroup& PreviousGroup, const FStackNodeGroup& NextGroup )

void FNiagaraStackGraphUtilities::FindAffectedScripts ( UNiagaraSystem* System, FVersionedNiagaraEmitter Emitter, UNiagaraNodeFunctionCall& ModuleNode, TArray< TWeakObjectPtr< UNiagaraScript > >& OutAffectedScripts )

TOptional< FMatchingFunctionInputData > FNiagaraStackGraphUtilities::FindAssignmentInputData ( const UNiagaraNodeAssignment& AssignmentNode, FName VariableName, TSharedRef< FNiagaraEmitterViewModel > EmitterViewModel )

UNiagaraNodeAssignment * FNiagaraStackGraphUtilities::FindAssignmentNode ( FGuid AssignmentNodeGuid, TSharedRef< FNiagaraEmitterViewModel > EmitterViewModel )

UNiagaraNodeFunctionCall * FNiagaraStackGraphUtilities::FindDynamicInputNodeForInput ( UNiagaraNodeFunctionCall& OwningFunctionNode, FName UnaliasedParameterName )

UNiagaraNodeFunctionCall * FNiagaraStackGraphUtilities::FindFunctionCallNode ( FGuid FunctionCallGuid, TSharedRef< FNiagaraEmitterViewModel > EmitterViewModel )

UNiagaraNodeFunctionCall * FNiagaraStackGraphUtilities::FindModuleNode ( FGuid ModuleNodeGuid, TSharedRef< FNiagaraEmitterViewModel > EmitterViewModel )

TArray< UNiagaraNodeFunctionCall * > FNiagaraStackGraphUtilities::FindModuleNodesForEventHandler ( FNiagaraEventScriptProperties& EventScriptProperties, TSharedRef< FNiagaraEmitterViewModel > EmitterViewModel )

TArray< UNiagaraNodeFunctionCall * > FNiagaraStackGraphUtilities::FindModuleNodesForSimulationStage ( UNiagaraSimulationStageBase& SimStage, TSharedRef< FNiagaraEmitterViewModel > EmitterViewModel )

bool FNiagaraStackGraphUtilities::FindScriptModulesInStack ( FAssetData ModuleScriptAsset, UNiagaraNodeOutput& TargetOutputNode, TArray< UNiagaraNodeFunctionCall* > OutFunctionCalls )

void FNiagaraStackGraphUtilities::FixDynamicInputNodeOutputPinsFromExternalChanges ( UNiagaraNodeFunctionCall& InFunctionCallNode )

void FNiagaraStackGraphUtilities::GatherInputRelationsForStack ( FInputDataCollection& State, TSharedRef< FNiagaraEmitterViewModel > EmitterViewModel )

void FNiagaraStackGraphUtilities::GatherRenamedStackFunctionInputAndOutputVariableNames ( FVersionedNiagaraEmitter Emitter, UNiagaraNodeFunctionCall& FunctionCallNode, const FString& OldFunctionName, const FString& NewFunctionName, TMap< FName, FName >& OutOldToNewNameMap )

void FNiagaraStackGraphUtilities::GatherRenamedStackFunctionOutputVariableNames ( FVersionedNiagaraEmitter Emitter, UNiagaraNodeFunctionCall& FunctionCallNode, const FString& OldFunctionName, const FString& NewFunctionName, TMap< FName, FName >& OutOldToNewNameMap )

TArray< UNiagaraNodeFunctionCall * > FNiagaraStackGraphUtilities::GetAllEventHandlerModuleNodes ( TSharedRef< FNiagaraEmitterViewModel > EmitterViewModel )

TArray< UNiagaraNodeFunctionCall * > FNiagaraStackGraphUtilities::GetAllModuleNodes ( TSharedRef< FNiagaraEmitterViewModel > EmitterViewModel )

TArray< UNiagaraNodeFunctionCall * > FNiagaraStackGraphUtilities::GetAllModuleNodes ( UNiagaraGraph* Graph )

TArray< UNiagaraNodeOutput * > FNiagaraStackGraphUtilities::GetAllOutputNodes ( TSharedRef< FNiagaraEmitterViewModel > EmitterViewModel )

TArray< UNiagaraNodeFunctionCall * > FNiagaraStackGraphUtilities::GetAllSimStagesModuleNodes ( TSharedRef< FNiagaraEmitterViewModel > EmitterViewModel )

void FNiagaraStackGraphUtilities::GetEmitterHandleAndCompiledScriptsForStackNode ( const UNiagaraSystem& OwningSystem, UNiagaraNode& StackNode, const FNiagaraEmitterHandle*& OutEmitterHandle, TArray< const UNiagaraScript* >& OutCompiledScripts )

UNiagaraNodeInput * FNiagaraStackGraphUtilities::GetEmitterInputNodeForStackNode ( UNiagaraNode& StackNode )

UNiagaraNodeOutput * FNiagaraStackGraphUtilities::GetEmitterOutputNodeForStackNode ( UNiagaraNode& StackNode )

const UNiagaraNodeOutput * FNiagaraStackGraphUtilities::GetEmitterOutputNodeForStackNode ( const UNiagaraNode& StackNode )

UEdGraphPin * FNiagaraStackGraphUtilities::GetLinkedValueHandleForFunctionInput ( const UEdGraphPin& OverridePin )

TOptional< bool > FNiagaraStackGraphUtilities::GetModuleIsEnabled ( UNiagaraNodeFunctionCall& FunctionCallNode )

TOptional< FName > FNiagaraStackGraphUtilities::GetNamespaceForOutputNode ( const UNiagaraNodeOutput* OutputNode )

TOptional< FName > FNiagaraStackGraphUtilities::GetNamespaceForScriptUsage ( ENiagaraScriptUsage ScriptUsage )

void FNiagaraStackGraphUtilities::GetNamespacesForNewReadParameters ( EStackEditContext EditContext, ENiagaraScriptUsage Usage, TArray< FName >& OutNamespacesForNewParameters )

void FNiagaraStackGraphUtilities::GetNamespacesForNewWriteParameters ( EStackEditContext EditContext, ENiagaraScriptUsage Usage, const TOptional< FName >& StackContextAlias, TArray< FName >& OutNamespacesForNewParameters )

void FNiagaraStackGraphUtilities::GetNewParameterAvailableTypes ( TArray< FNiagaraTypeDefinition >& OutAvailableTypes, FName Namespace )

UNiagaraNodeFunctionCall * FNiagaraStackGraphUtilities::GetNextModuleNode ( UNiagaraNodeFunctionCall& CurrentNode )

UEdGraphPin & FNiagaraStackGraphUtilities::GetOrCreateStackFunctionInputOverridePin ( UNiagaraNodeFunctionCall& StackFunctionCall, FNiagaraParameterHandle AliasedInputParameterHandle, FNiagaraTypeDefinition InputType, const FGuid& InputScriptVariableId, const FGuid& PreferredOverrideNodeGuid )

UNiagaraNodeParameterMapSet & FNiagaraStackGraphUtilities::GetOrCreateStackFunctionOverrideNode ( UNiagaraNodeFunctionCall& FunctionCallNode, const FGuid& PreferredOverrideNodeGuid )

void FNiagaraStackGraphUtilities::GetOrderedModuleNodes ( UNiagaraNodeOutput& OutputNode, TArray< UNiagaraNodeFunctionCall* >& ModuleNodes )

ENiagaraScriptUsage FNiagaraStackGraphUtilities::GetOutputNodeUsage ( const UNiagaraNode& StackNode )

TArray< UEdGraphPin * > FNiagaraStackGraphUtilities::GetOverridePinsForFunction ( UNiagaraNodeParameterMapSet& OverrideNode, UNiagaraNodeFunctionCall& FunctionCallNode )

UEdGraphPin * FNiagaraStackGraphUtilities::GetParameterMapInputPin ( UNiagaraNode& Node )

const UEdGraphPin * FNiagaraStackGraphUtilities::GetParameterMapInputPin ( const UNiagaraNode& Node )

UEdGraphPin * FNiagaraStackGraphUtilities::GetParameterMapOutputPin ( UNiagaraNode& Node )

void FNiagaraStackGraphUtilities::GetParametersForContext ( UEdGraph* Graph, UNiagaraSystem& System, TSet< FNiagaraVariableBase >& OutParameters )

UNiagaraNodeFunctionCall * FNiagaraStackGraphUtilities::GetPreviousModuleNode ( UNiagaraNodeFunctionCall& CurrentNode )

FGuid FNiagaraStackGraphUtilities::GetScriptVariableIdForLinkedModuleParameter ( const FNiagaraVariableBase& LinkedParameter, UNiagaraGraph& TargetGraph )

bool FNiagaraStackGraphUtilities::GetStackFunctionInputAndOutputVariables ( UNiagaraNodeFunctionCall& FunctionCallNode, FCompileConstantResolver ConstantResolver, TArray< FNiagaraVariable >& OutVariables, TArray< FNiagaraVariable >& OutVariablesWithOriginalAliasesIntact )

UEdGraphPin * FNiagaraStackGraphUtilities::GetStackFunctionInputOverridePin ( UNiagaraNodeFunctionCall& StackFunctionCall, FNiagaraParameterHandle AliasedInputParameterHandle )

void FNiagaraStackGraphUtilities::GetStackFunctionInputPinsWithoutCache ( const UNiagaraNodeFunctionCall& FunctionCallNode, TConstArrayView< FNiagaraVariable > StaticVars, TArray< const UEdGraphPin* >& OutInputPins, const FCompileConstantResolver& ConstantResolver, ENiagaraGetStackFunctionInputPinsOptions Options, bool bIgnoreDisabled, bool bFilterForCompilation )

void FNiagaraStackGraphUtilities::GetStackFunctionInputs ( const UNiagaraNodeFunctionCall& FunctionCallNode, TArray< FNiagaraVariable >& OutInputVariables, ENiagaraGetStackFunctionInputPinsOptions Options, bool bIgnoreDisabled )

void FNiagaraStackGraphUtilities::GetStackFunctionInputs ( const UNiagaraNodeFunctionCall& FunctionCallNode, TArray< FNiagaraVariable >& OutInputVariables, FCompileConstantResolver ConstantResolver, ENiagaraGetStackFunctionInputPinsOptions Options, bool bIgnoreDisabled )

void FNiagaraStackGraphUtilities::GetStackFunctionInputs ( const UNiagaraNodeFunctionCall& FunctionCallNode, TArray< FNiagaraVariable >& OutInputVariables, TSet< FNiagaraVariable >& OutHiddenVariables, FCompileConstantResolver ConstantResolver, ENiagaraGetStackFunctionInputPinsOptions Options, bool bIgnoreDisabled )

void FNiagaraStackGraphUtilities::GetStackFunctionInputsLegacy ( const UNiagaraNodeFunctionCall& FunctionCallNode, TArray< FNiagaraVariable >& OutInputVariables, ENiagaraGetStackFunctionInputPinsOptions Options, bool bIgnoreDisabled )

void FNiagaraStackGraphUtilities::GetStackFunctionInputsLegacy ( const UNiagaraNodeFunctionCall& FunctionCallNode, TArray< FNiagaraVariable >& OutInputVariables, FCompileConstantResolver ConstantResolver, ENiagaraGetStackFunctionInputPinsOptions Options, bool bIgnoreDisabled )

void FNiagaraStackGraphUtilities::GetStackFunctionInputsLegacy ( const UNiagaraNodeFunctionCall& FunctionCallNode, TArray< FNiagaraVariable >& OutInputVariables, TSet< FNiagaraVariable >& OutHiddenVariables, FCompileConstantResolver ConstantResolver, ENiagaraGetStackFunctionInputPinsOptions Options, bool bIgnoreDisabled )

void FNiagaraStackGraphUtilities::GetStackFunctionOutputVariables ( UNiagaraNodeFunctionCall& FunctionCallNode, FCompileConstantResolver ConstantResolver, TArray< FNiagaraVariable >& OutOutputVariables, TArray< FNiagaraVariable >& OutOutputVariablesWithOriginalAliasesIntact )

UNiagaraNodeParameterMapSet * FNiagaraStackGraphUtilities::GetStackFunctionOverrideNode ( UNiagaraNodeFunctionCall& FunctionCallNode )

void FNiagaraStackGraphUtilities::GetStackFunctionStaticSwitchPins ( const UNiagaraNodeFunctionCall& FunctionCallNode, TArray< UEdGraphPin* >& OutInputPins, TSet< UEdGraphPin* >& OutHiddenPins, FCompileConstantResolver& ConstantResolver )

void FNiagaraStackGraphUtilities::GetStackFunctionStaticSwitchPinsLegacy ( const UNiagaraNodeFunctionCall& FunctionCallNode, TArray< UEdGraphPin* >& OutInputPins, TSet< UEdGraphPin* >& OutHiddenPins, FCompileConstantResolver& ConstantResolver )

bool FNiagaraStackGraphUtilities::GetStackIssuesRecursively ( const UNiagaraStackEntry*const Entry, TArray< UNiagaraStackErrorItem* >& OutIssues )

void FNiagaraStackGraphUtilities::GetStackNodeGroups ( UNiagaraNode& StackNode, TArray< FStackNodeGroup >& OutStackNodeGroups )

uint32 FNiagaraStackGraphUtilities::GetTypeHash ( const FInputDataCacheKey& InputDataCacheKey )

TArray< UEdGraphPin * > FNiagaraStackGraphUtilities::GetUnusedFunctionInputPins ( const UNiagaraNodeFunctionCall& FunctionCallNode, FCompileConstantResolver ConstantResolver )

void FNiagaraStackGraphUtilities::InitializeStackFunctionInput ( TSharedRef< FNiagaraSystemViewModel > SystemViewModel, TSharedPtr< FNiagaraEmitterViewModel > EmitterViewModel, UNiagaraStackEditorData& StackEditorData, UNiagaraNodeFunctionCall& ModuleNode, UNiagaraNodeFunctionCall& InputFunctionCallNode, FName InputName )

void FNiagaraStackGraphUtilities::InitializeStackFunctionInputs ( TSharedRef< FNiagaraSystemViewModel > SystemViewModel, TSharedPtr< FNiagaraEmitterViewModel > EmitterViewModel, UNiagaraStackEditorData& StackEditorData, UNiagaraNodeFunctionCall& ModuleNode, UNiagaraNodeFunctionCall& InputFunctionCallNode )

bool FNiagaraStackGraphUtilities::IsOverridePinForFunction ( UEdGraphPin& OverridePin, UNiagaraNodeFunctionCall& FunctionCallNode )

bool FNiagaraStackGraphUtilities::IsRapidIterationType ( const FNiagaraTypeDefinition& InputType )

bool FNiagaraStackGraphUtilities::IsValidDefaultDynamicInput ( UNiagaraScript& OwningScript, UEdGraphPin& DefaultPin )

void FNiagaraStackGraphUtilities::MakeLinkTo ( UEdGraphPin* PinA, UEdGraphPin* PinB )

void FNiagaraStackGraphUtilities::MoveModule ( UNiagaraScript& SourceScript, UNiagaraNodeFunctionCall& ModuleToMove, UNiagaraSystem& TargetSystem, FGuid TargetEmitterHandleId, ENiagaraScriptUsage TargetUsage, FGuid TargetUsageId, int32 TargetModuleIndex, bool bForceCopy, UNiagaraNodeFunctionCall*& OutMovedModue )

bool FNiagaraStackGraphUtilities::ParameterAllowedInExecutionCategory ( const FName InParameterName, const FName ExecutionCategory )

void FNiagaraStackGraphUtilities::PopulateFunctionCallNameBindings ( UNiagaraNodeFunctionCall& InFunctionCallNode )

void FNiagaraStackGraphUtilities::RebuildEmitterNodes ( UNiagaraSystem& System )

void FNiagaraStackGraphUtilities::RelayoutGraph ( UEdGraph& Graph )

bool FNiagaraStackGraphUtilities::RemoveModuleFromStack ( UNiagaraScript& OwningScript, UNiagaraNodeFunctionCall& ModuleNode )

bool FNiagaraStackGraphUtilities::RemoveModuleFromStack ( UNiagaraSystem& OwningSystem, FGuid OwningEmitterId, UNiagaraNodeFunctionCall& ModuleNode )

bool FNiagaraStackGraphUtilities::RemoveModuleFromStack ( UNiagaraScript& OwningScript, UNiagaraNodeFunctionCall& ModuleNode, TArray< TWeakObjectPtr< UNiagaraNodeInput > >& OutRemovedInputNodes )

bool FNiagaraStackGraphUtilities::RemoveModuleFromStack ( UNiagaraSystem& OwningSystem, FGuid OwningEmitterId, UNiagaraNodeFunctionCall& ModuleNode, TArray< TWeakObjectPtr< UNiagaraNodeInput > >& OutRemovedInputNodes )

void FNiagaraStackGraphUtilities::RemoveNodesForStackFunctionInputOverridePin ( UEdGraphPin& StackFunctionInputOverridePin )

void FNiagaraStackGraphUtilities::RemoveNodesForStackFunctionInputOverridePin ( UEdGraphPin& StackFunctinoInputOverridePin, TArray< TWeakObjectPtr< UNiagaraDataInterface > >& OutRemovedDataObjects )

void FNiagaraStackGraphUtilities::RenameAssignmentTarget ( UNiagaraSystem& OwningSystem, FVersionedNiagaraEmitter OwningEmitter, UNiagaraScript& OwningScript, UNiagaraNodeAssignment& OwningAssignmentNode, FNiagaraVariable CurrentAssignmentTarget, FName NewAssignmentTargetName )

void FNiagaraStackGraphUtilities::RenameReferencingParameters ( UNiagaraSystem* System, FVersionedNiagaraEmitter Emitter, UNiagaraNodeFunctionCall& FunctionCallNode, const FString& OldName, const FString& NewName )

UNiagaraNodeOutput * FNiagaraStackGraphUtilities::ResetGraphForOutput ( UNiagaraGraph& NiagaraGraph, ENiagaraScriptUsage ScriptUsage, FGuid ScriptUsageId, const FGuid& PreferredOutputNodeGuid, const FGuid& PreferredInputNodeGuid )

void FNiagaraStackGraphUtilities::SetCustomExpressionForFunctionInput ( UEdGraphPin& OverridePin, const FString& CustomExpression, UNiagaraNodeCustomHlsl*& OutDynamicInputFunctionCall, const FGuid& NewNodePersistentId )

void FNiagaraStackGraphUtilities::SetDataInterfaceValueForFunctionInput ( UEdGraphPin& OverridePin, UClass* DataObjectType, FString InputNodeInputName, UNiagaraDataInterface*& OutDataObject, const FGuid& NewNodePersistentId )

void FNiagaraStackGraphUtilities::SetDynamicInputForFunctionInput ( UEdGraphPin& OverridePin, UNiagaraScript* DynamicInput, UNiagaraNodeFunctionCall*& OutDynamicInputFunctionCall, const FGuid& NewNodePersistentId, FString SuggestedName, const FGuid& InScriptVersion )

void FNiagaraStackGraphUtilities::SetLinkedParameterValueForFunctionInput ( UEdGraphPin& OverridePin, const FNiagaraVariableBase& LinkedParameter, const TSet< FNiagaraVariableBase >& KnownParameters, ENiagaraDefaultMode DesiredDefaultMode, const FGuid& NewNodePersistentId )

void FNiagaraStackGraphUtilities::SetModuleIsEnabled ( UNiagaraNodeFunctionCall& FunctionCallNode, bool bIsEnabled )

void FNiagaraStackGraphUtilities::SetObjectAssetValueForFunctionInput ( UEdGraphPin& OverridePin, UClass* DataObjectType, FString InputNodeInputName, UObject* ObjectAsset, const FGuid& NewNodePersistentId )

TArray< FName > FNiagaraStackGraphUtilities::StackContextResolution ( FVersionedNiagaraEmitter OwningEmitter, UNiagaraNodeOutput* OutputNodeInChain )

FString FNiagaraStackGraphUtilities::StackKeys::GenerateStackFunctionInputEditorDataKey ( const UNiagaraNodeFunctionCall& FunctionCallNode, FNiagaraParameterHandle InputParameterHandle )

FString FNiagaraStackGraphUtilities::StackKeys::GenerateStackModuleEditorDataKey ( const UNiagaraNodeFunctionCall& ModuleNode )

FString FNiagaraStackGraphUtilities::StackKeys::GenerateStackRendererEditorDataKey ( const UNiagaraRendererProperties& Renderer )

void FNiagaraStackGraphUtilities::SynchronizeReferencingMapPinsWithFunctionCall ( UNiagaraNodeFunctionCall& InFunctionCallNode )

void FNiagaraStackGraphUtilities::SynchronizeVariableToLibraryAndApplyToGraph ( UNiagaraScriptVariable* ScriptVarToSync )

bool FNiagaraStackGraphUtilities::TryRenameAssignmentTarget ( UNiagaraNodeAssignment& OwningAssignmentNode, FNiagaraVariable CurrentAssignmentTarget, FName NewAssignmentTargetName )

bool FNiagaraStackGraphUtilities::ValidateGraphForOutput ( UNiagaraGraph& NiagaraGraph, ENiagaraScriptUsage ScriptUsage, FGuid ScriptUsageId, FText& ErrorMessage )

FReply FNiagaraSystemToolkitParameterPanelUtilities::CreateDragEventForParameterItem ( const FNiagaraParameterPanelItemBase& DraggedItem, const FPointerEvent& MouseEvent, const TArray< FNiagaraGraphParameterReference >& GraphParameterReferencesForItem, const TSharedPtr< TArray< FName > >& ParametersWithNamespaceModifierRenamePending )

uint32 GetTypeHash ( const FNiagaraActionIdentifier& Identity )

uint32 GetTypeHash ( const FReservedParameter& ReservedParameter )

uint32 GetTypeHash ( const FNiagaraNamespaceMetadata& NamespaceMetaData )

uint32 GetTypeHash ( const FNiagaraParameterHandle& Var )

uint32 GetTypeHash ( const UNiagaraStackFunctionInput::FNiagaraAvailableParameterInfo& ParameterInfo )

void NiagaraValidation::AddGoToFXTypeLink ( FNiagaraValidationResult& Result, UNiagaraEffectType* FXType )

TArray< FNiagaraPlatformSetConflictInfo > NiagaraValidation::GatherPlatformSetConflicts ( const FNiagaraPlatformSet* SetA, const FNiagaraPlatformSet* SetB )

TArray< T * > NiagaraValidation::GetAllStackEntriesInSystem ( TSharedPtr< FNiagaraSystemViewModel > ViewModel, bool bRefresh )

TSharedPtr< FNiagaraEmitterHandleViewModel > NiagaraValidation::GetEmitterViewModel ( const FNiagaraValidationContext& Context, UNiagaraEmitter* NiagaraEmitter )

TOptional< int32 > NiagaraValidation::GetModuleStaticInt32Value ( const UNiagaraStackModuleItem* Module, FName ParameterName )

FString NiagaraValidation::GetPlatformConflictsString ( TConstArrayView< FNiagaraPlatformSetConflictInfo > ConflictInfos, int MaxPlatformsToShow )

FString NiagaraValidation::GetPlatformConflictsString ( const FNiagaraPlatformSet& PlatformSetA, const FNiagaraPlatformSet& PlatformSetB, int MaxPlatformsToShow )

UNiagaraStackRendererItem * NiagaraValidation::GetRendererStackItem ( UNiagaraStackViewModel* StackViewModel, UNiagaraRendererProperties* RendererProperties )

TArray< T * > NiagaraValidation::GetStackEntries ( UNiagaraStackViewModel* StackViewModel, bool bRefresh )

T * NiagaraValidation::GetStackEntry ( UNiagaraStackViewModel* StackViewModel, bool bRefresh )

bool NiagaraValidation::HasValidationRules ( UNiagaraSystem* NiagaraSystem )

FNiagaraValidationFix NiagaraValidation::MakeDisableGPUSimulationFix ( FVersionedNiagaraEmitterWeakPtr WeakEmitterPtr )

void NiagaraValidation::SetModuleStaticInt32Value ( UNiagaraStackModuleItem* Module, FName ParameterName, int32 NewValue )

bool NiagaraValidation::StructContainsUObjectProperty ( UStruct* Struct )

void NiagaraValidation::ValidateAllRulesInSystem ( TSharedPtr< FNiagaraSystemViewModel > ViewModel, TFunction< void(const FNiagaraValidationResult&Result)> ResultCallback )

UEdGraphPin * UE::Niagara::Wizard::Utilities::AddReadParameterPin ( const FNiagaraTypeDefinition& Type, const FName& Name, UNiagaraNodeParameterMapGet* MapGetNode )

UEdGraphPin * UE::Niagara::Wizard::Utilities::AddWriteParameterPin ( const FNiagaraTypeDefinition& Type, const FName& Name, UNiagaraNodeParameterMapSet* MapSetNode )

UNiagaraNodeFunctionCall * UE::Niagara::Wizard::Utilities::CreateDataInterfaceFunctionNode ( const TSubclassOf< UNiagaraDataInterface >& DataInterfaceClass, const FName& FunctionName, UNiagaraGraph* Graph )

TSharedRef< IDetailsView > UE::Niagara::Wizard::Utilities::CreateDetailsView()

UNiagaraNodeFunctionCall * UE::Niagara::Wizard::Utilities::CreateFunctionCallNode ( UNiagaraScript* FunctionScript, UNiagaraGraph* Graph )

UNiagaraNodeOp * UE::Niagara::Wizard::Utilities::CreateOpNode ( const FName& OpName, UNiagaraGraph* Graph )

NodeType * UE::Niagara::Wizard::Utilities::FindSingleNodeChecked ( UNiagaraGraph* Graph )

void UE::Niagara::Wizard::Utilities::SetDefaultBinding ( UNiagaraGraph* Graph, const FName& VarName, const FName& DefaultBinding )

void UE::Niagara::Wizard::Utilities::SetDefaultValue ( UNiagaraGraph* Graph, const FName& VarName, const FNiagaraTypeDefinition& TypeDef, T Value )

void UE::Niagara::Wizard::Utilities::SetTooltip ( UNiagaraGraph* Graph, const FName& VarName, const FText& Tooltip )



---

## NiagaraFluids

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NiagaraFluids

**Contents:**
- NiagaraFluids
- Navigation
- Interfaces



---

## NiagaraPreviewContent

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NiagaraPreviewContent

**Contents:**
- NiagaraPreviewContent
- Navigation
- Classes



---

## NiagaraShader

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NiagaraShader

**Contents:**
- NiagaraShader
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

void DumpComputeShaderStats ( EShaderPlatform Platform )

FNiagaraCompileEventSeverity FNiagaraCVarUtilities::GetCompileEventSeverityForFailIfNotSet()

bool FNiagaraCVarUtilities::GetShouldEmitMessagesForFailIfNotSet()

void FNiagaraDistanceFieldHelper::SetGlobalDistanceFieldParameters ( const FGlobalDistanceFieldParameterData* OptionalParameterData, FGlobalDistanceFieldParameters2& ShaderParameters )

RENDERER_API const FShaderParametersMetadata * GetForwardDeclaredShaderParametersStructMetadata ( const FSceneUniformParameters* DummyPtr )

void NiagaraClearCounts::ClearCountsInt ( FRDGBuilder& GraphBuilder, FRDGBufferUAVRef UAV, TConstArrayView< TPair< uint32, int32 > > IndexAndValueArray )

void NiagaraClearCounts::ClearCountsInt ( FRHICommandList& RHICmdList, FRHIUnorderedAccessView* UAV, TConstArrayView< TPair< uint32, int32 > > IndexAndValueArray )

void NiagaraClearCounts::ClearCountsUInt ( FRDGBuilder& GraphBuilder, FRDGBufferUAVRef UAV, TConstArrayView< TPair< uint32, uint32 > > IndexAndValueArray )

void NiagaraClearCounts::ClearCountsUInt ( FRHICommandList& RHICmdList, FRHIUnorderedAccessView* UAV, TConstArrayView< TPair< uint32, uint32 > > IndexAndValueArray )

void NiagaraComputeGPUFreeIDs ( FRHICommandList& RHICmdList, ERHIFeatureLevel::Type FeatureLevel, FRHIShaderResourceView* IDToIndexTableSRV, uint32 NumIDs, FRHIUnorderedAccessView* FreeIDUAV, FRHIUnorderedAccessView* FreeIDListSizesUAV, uint32 FreeIDListIndex )

void NiagaraDebugShaders::ClearUAV ( FRDGBuilder& GraphBuilder, FRDGBufferUAVRef UAV, FUintVector4 ClearValues, uint32 UIntsToSet )

void NiagaraDebugShaders::DrawDebugLines ( FRDGBuilder& GraphBuilder, const FSceneView& View, FRDGTextureRef SceneColor, FRDGTextureRef SceneDepth, const uint32 LineInstanceCount, FRDGBufferRef LineBuffer )

void NiagaraDebugShaders::DrawDebugLines ( FRDGBuilder& GraphBuilder, const FSceneView& View, FRDGTextureRef SceneColor, FRDGTextureRef SceneDepth, FRDGBufferRef ArgsBuffer, FRDGBufferRef LineBuffer )

void NiagaraDebugShaders::VisualizeTexture ( FRDGBuilder& GraphBuilder, const FSceneView& View, const FScreenPassRenderTarget& Output, const FIntPoint& Location, const int32& DisplayHeight, const FIntVector4& AttributesToVisualize, FRDGTextureRef Texture, const FIntVector4& NumTextureAttributes, uint32 TickCounter, const FVector2D& PreviewDisplayRange )

void NiagaraFillGPUIntBuffer ( FRHICommandList& RHICmdList, ERHIFeatureLevel::Type FeatureLevel, FRHIUnorderedAccessView* BufferUAV, uint32 NumElements, int32 FillValue )

void NiagaraGenerateMips::GenerateMips ( FRDGBuilder& GraphBuilder, FRDGTextureRef RDGTexture, ENiagaraMipMapGenerationType GenType )

void NiagaraInitGPUFreeIDList ( FRHICommandList& RHICmdList, ERHIFeatureLevel::Type FeatureLevel, FRHIUnorderedAccessView* NewBufferUAV, uint32 NewBufferNumElements, FRHIShaderResourceView* ExistingBufferSRV, uint32 ExistingBufferNumElements )

void UpdateNiagaraShaderCompilingStats ( const FNiagaraShaderScript* Script )



---

## NiagaraSimCachingEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NiagaraSimCachingEditor

**Contents:**
- NiagaraSimCachingEditor
- Navigation
- Classes
- Interfaces



---

## NiagaraSimCaching

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NiagaraSimCaching

**Contents:**
- NiagaraSimCaching
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## NiagaraVertexFactories

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NiagaraVertexFactories

**Contents:**
- NiagaraVertexFactories
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Variables
  - Public
- Functions

BEGIN_GLOBAL_SHADER_PARAMETER_STRUCT ( FNiagaraRibbonUniformParameters, NIAGARAVERTEXFACTORIES_API )

BEGIN_GLOBAL_SHADER_PARAMETER_STRUCT ( FNiagaraRibbonVFLooseParameters, NIAGARAVERTEXFACTORIES_API )

BEGIN_GLOBAL_SHADER_PARAMETER_STRUCT ( FNiagaraSpriteUniformParameters, NIAGARAVERTEXFACTORIES_API )

BEGIN_GLOBAL_SHADER_PARAMETER_STRUCT ( FNiagaraSpriteVFLooseParameters, NIAGARAVERTEXFACTORIES_API )

BEGIN_SHADER_PARAMETER_STRUCT ( FNiagaraMeshCommonParameters, NIAGARAVERTEXFACTORIES_API )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset PrevCameraOffsetDataOffset DefaultRotation DefaultVelocity DefaultPrevScale DefaultPrevPosition DefaultPrevCameraOffset NIAGARAVERTEXFACTORIES_API VertexFetch_TexCoordBuffer VertexFetch_ColorComponentsBuffer SubImageSize TexCoordWeightB NormalizedAgeDataOffset MaterialRandomDataOffset MaterialParamDataOffset MaterialParam2DataOffset DefaultNormAge DefaultMatRandom DefaultDynamicMaterialParameter0 DefaultDynamicMaterialParameter2 SubImageBlendMode END_GLOBAL_SHADER_PARAMETER_STRUCT ()

CutoutParameters ParticleAlignmentMode SortedIndicesOffset CutoutGeometry NiagaraParticleDataHalf IndirectArgsBuffer END_GLOBAL_SHADER_PARAMETER_STRUCT ()

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset PrevCameraOffsetDataOffset DefaultRotation DefaultVelocity DefaultPrevScale DefaultPrevPosition DefaultPrevCameraOffset END_SHADER_PARAMETER_STRUCT()

ENUM_CLASS_FLAGS ( ENiagaraDrawIndirectArgGenTaskFlags )

NiagaraParticleDataFloat NiagaraParticleDataInt SHADER_PARAMETER ( uint32, NiagaraFloatDataStride )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset SHADER_PARAMETER ( FVector3f, SystemLWCTile )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace SHADER_PARAMETER ( int, AccurateMotionVectors )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds SHADER_PARAMETER ( uint32, FacingMode )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale SHADER_PARAMETER ( FVector3f, MeshOffset )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation SHADER_PARAMETER ( int, bMeshOffsetIsWorldSpace )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable SHADER_PARAMETER ( FVector3f, LockedAxis )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace SHADER_PARAMETER ( int, ScaleDataOffset )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset SHADER_PARAMETER ( int, PositionDataOffset )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset SHADER_PARAMETER ( int, CameraOffsetDataOffset )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset SHADER_PARAMETER ( int, PrevRotationDataOffset )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset SHADER_PARAMETER ( int, PrevVelocityDataOffset )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset PrevCameraOffsetDataOffset SHADER_PARAMETER ( FVector3f, DefaultScale )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset PrevCameraOffsetDataOffset DefaultRotation SHADER_PARAMETER ( FVector3f, DefaultPosition )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset PrevCameraOffsetDataOffset DefaultRotation DefaultVelocity SHADER_PARAMETER ( float, DefaultCameraOffset )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset PrevCameraOffsetDataOffset DefaultRotation DefaultVelocity DefaultPrevScale SHADER_PARAMETER ( FVector4f, DefaultPrevRotation )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset PrevCameraOffsetDataOffset DefaultRotation DefaultVelocity DefaultPrevScale DefaultPrevPosition SHADER_PARAMETER ( FVector3f, DefaultPrevVelocity )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset PrevCameraOffsetDataOffset DefaultRotation DefaultVelocity DefaultPrevScale DefaultPrevPosition DefaultPrevCameraOffset NIAGARAVERTEXFACTORIES_API VertexFetch_TexCoordBuffer VertexFetch_ColorComponentsBuffer SHADER_PARAMETER ( FIntVector4, VertexFetch_Parameters )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset PrevCameraOffsetDataOffset DefaultRotation DefaultVelocity DefaultPrevScale DefaultPrevPosition DefaultPrevCameraOffset NIAGARAVERTEXFACTORIES_API VertexFetch_TexCoordBuffer VertexFetch_ColorComponentsBuffer SubImageSize SHADER_PARAMETER ( uint32, TexCoordWeightA )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset PrevCameraOffsetDataOffset DefaultRotation DefaultVelocity DefaultPrevScale DefaultPrevPosition DefaultPrevCameraOffset NIAGARAVERTEXFACTORIES_API VertexFetch_TexCoordBuffer VertexFetch_ColorComponentsBuffer SubImageSize TexCoordWeightB SHADER_PARAMETER ( uint32, MaterialParamValidMask )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset PrevCameraOffsetDataOffset DefaultRotation DefaultVelocity DefaultPrevScale DefaultPrevPosition DefaultPrevCameraOffset NIAGARAVERTEXFACTORIES_API VertexFetch_TexCoordBuffer VertexFetch_ColorComponentsBuffer SubImageSize TexCoordWeightB NormalizedAgeDataOffset SHADER_PARAMETER ( int, SubImageDataOffset )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset PrevCameraOffsetDataOffset DefaultRotation DefaultVelocity DefaultPrevScale DefaultPrevPosition DefaultPrevCameraOffset NIAGARAVERTEXFACTORIES_API VertexFetch_TexCoordBuffer VertexFetch_ColorComponentsBuffer SubImageSize TexCoordWeightB NormalizedAgeDataOffset MaterialRandomDataOffset SHADER_PARAMETER ( int, ColorDataOffset )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset PrevCameraOffsetDataOffset DefaultRotation DefaultVelocity DefaultPrevScale DefaultPrevPosition DefaultPrevCameraOffset NIAGARAVERTEXFACTORIES_API VertexFetch_TexCoordBuffer VertexFetch_ColorComponentsBuffer SubImageSize TexCoordWeightB NormalizedAgeDataOffset MaterialRandomDataOffset MaterialParamDataOffset SHADER_PARAMETER ( int, MaterialParam1DataOffset )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset PrevCameraOffsetDataOffset DefaultRotation DefaultVelocity DefaultPrevScale DefaultPrevPosition DefaultPrevCameraOffset NIAGARAVERTEXFACTORIES_API VertexFetch_TexCoordBuffer VertexFetch_ColorComponentsBuffer SubImageSize TexCoordWeightB NormalizedAgeDataOffset MaterialRandomDataOffset MaterialParamDataOffset MaterialParam2DataOffset SHADER_PARAMETER ( int, MaterialParam3DataOffset )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset PrevCameraOffsetDataOffset DefaultRotation DefaultVelocity DefaultPrevScale DefaultPrevPosition DefaultPrevCameraOffset NIAGARAVERTEXFACTORIES_API VertexFetch_TexCoordBuffer VertexFetch_ColorComponentsBuffer SubImageSize TexCoordWeightB NormalizedAgeDataOffset MaterialRandomDataOffset MaterialParamDataOffset MaterialParam2DataOffset DefaultNormAge SHADER_PARAMETER ( float, DefaultSubImage )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset PrevCameraOffsetDataOffset DefaultRotation DefaultVelocity DefaultPrevScale DefaultPrevPosition DefaultPrevCameraOffset NIAGARAVERTEXFACTORIES_API VertexFetch_TexCoordBuffer VertexFetch_ColorComponentsBuffer SubImageSize TexCoordWeightB NormalizedAgeDataOffset MaterialRandomDataOffset MaterialParamDataOffset MaterialParam2DataOffset DefaultNormAge DefaultMatRandom SHADER_PARAMETER ( FVector4f, DefaultColor )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset PrevCameraOffsetDataOffset DefaultRotation DefaultVelocity DefaultPrevScale DefaultPrevPosition DefaultPrevCameraOffset NIAGARAVERTEXFACTORIES_API VertexFetch_TexCoordBuffer VertexFetch_ColorComponentsBuffer SubImageSize TexCoordWeightB NormalizedAgeDataOffset MaterialRandomDataOffset MaterialParamDataOffset MaterialParam2DataOffset DefaultNormAge DefaultMatRandom DefaultDynamicMaterialParameter0 SHADER_PARAMETER ( FVector4f, DefaultDynamicMaterialParameter1 )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset PrevCameraOffsetDataOffset DefaultRotation DefaultVelocity DefaultPrevScale DefaultPrevPosition DefaultPrevCameraOffset NIAGARAVERTEXFACTORIES_API VertexFetch_TexCoordBuffer VertexFetch_ColorComponentsBuffer SubImageSize TexCoordWeightB NormalizedAgeDataOffset MaterialRandomDataOffset MaterialParamDataOffset MaterialParam2DataOffset DefaultNormAge DefaultMatRandom DefaultDynamicMaterialParameter0 DefaultDynamicMaterialParameter2 SHADER_PARAMETER ( FVector4f, DefaultDynamicMaterialParameter3 )

CameraRight SHADER_PARAMETER ( FVector4f, CameraUp )

CameraRight ScreenAlignment SHADER_PARAMETER ( int, PositionDataOffset )

CameraRight ScreenAlignment PrevPositionDataOffset SHADER_PARAMETER ( int, VelocityDataOffset )

CameraRight ScreenAlignment PrevPositionDataOffset WidthDataOffset SHADER_PARAMETER ( int, PrevWidthDataOffset )

CameraRight ScreenAlignment PrevPositionDataOffset WidthDataOffset TwistDataOffset SHADER_PARAMETER ( int, PrevTwistDataOffset )

CameraRight ScreenAlignment PrevPositionDataOffset WidthDataOffset TwistDataOffset ColorDataOffset SHADER_PARAMETER ( int, FacingDataOffset )

CameraRight ScreenAlignment PrevPositionDataOffset WidthDataOffset TwistDataOffset ColorDataOffset PrevFacingDataOffset SHADER_PARAMETER ( int, NormalizedAgeDataOffset )

CameraRight ScreenAlignment PrevPositionDataOffset WidthDataOffset TwistDataOffset ColorDataOffset PrevFacingDataOffset MaterialRandomDataOffset SHADER_PARAMETER ( uint32, MaterialParamValidMask )

CameraRight ScreenAlignment PrevPositionDataOffset WidthDataOffset TwistDataOffset ColorDataOffset PrevFacingDataOffset MaterialRandomDataOffset MaterialParamDataOffset SHADER_PARAMETER ( int, MaterialParam1DataOffset )

CameraRight ScreenAlignment PrevPositionDataOffset WidthDataOffset TwistDataOffset ColorDataOffset PrevFacingDataOffset MaterialRandomDataOffset MaterialParamDataOffset MaterialParam2DataOffset SHADER_PARAMETER ( int, MaterialParam3DataOffset )

CameraRight ScreenAlignment PrevPositionDataOffset WidthDataOffset TwistDataOffset ColorDataOffset PrevFacingDataOffset MaterialRandomDataOffset MaterialParamDataOffset MaterialParam2DataOffset DistanceFromStartOffset SHADER_PARAMETER ( int, U0OverrideDataOffset )

CameraRight ScreenAlignment PrevPositionDataOffset WidthDataOffset TwistDataOffset ColorDataOffset PrevFacingDataOffset MaterialRandomDataOffset MaterialParamDataOffset MaterialParam2DataOffset DistanceFromStartOffset V0RangeOverrideDataOffset SHADER_PARAMETER ( int, U1OverrideDataOffset )

CameraRight ScreenAlignment PrevPositionDataOffset WidthDataOffset TwistDataOffset ColorDataOffset PrevFacingDataOffset MaterialRandomDataOffset MaterialParamDataOffset MaterialParam2DataOffset DistanceFromStartOffset V0RangeOverrideDataOffset V1RangeOverrideDataOffset SHADER_PARAMETER ( int, InterpCount )

CameraRight ScreenAlignment PrevPositionDataOffset WidthDataOffset TwistDataOffset ColorDataOffset PrevFacingDataOffset MaterialRandomDataOffset MaterialParamDataOffset MaterialParam2DataOffset DistanceFromStartOffset V0RangeOverrideDataOffset V1RangeOverrideDataOffset OneOverInterpCount SHADER_PARAMETER ( int, ParticleIdShift )

CameraRight ScreenAlignment PrevPositionDataOffset WidthDataOffset TwistDataOffset ColorDataOffset PrevFacingDataOffset MaterialRandomDataOffset MaterialParamDataOffset MaterialParam2DataOffset DistanceFromStartOffset V0RangeOverrideDataOffset V1RangeOverrideDataOffset OneOverInterpCount ParticleIdMask SHADER_PARAMETER ( int, InterpIdShift )

CameraRight ScreenAlignment PrevPositionDataOffset WidthDataOffset TwistDataOffset ColorDataOffset PrevFacingDataOffset MaterialRandomDataOffset MaterialParamDataOffset MaterialParam2DataOffset DistanceFromStartOffset V0RangeOverrideDataOffset V1RangeOverrideDataOffset OneOverInterpCount ParticleIdMask InterpIdMask SHADER_PARAMETER ( int, SliceVertexIdMask )

CameraRight ScreenAlignment PrevPositionDataOffset WidthDataOffset TwistDataOffset ColorDataOffset PrevFacingDataOffset MaterialRandomDataOffset MaterialParamDataOffset MaterialParam2DataOffset DistanceFromStartOffset V0RangeOverrideDataOffset V1RangeOverrideDataOffset OneOverInterpCount ParticleIdMask InterpIdMask ShouldFlipNormalToView SHADER_PARAMETER ( int, ShouldUseMultiRibbon )

CameraRight ScreenAlignment PrevPositionDataOffset WidthDataOffset TwistDataOffset ColorDataOffset PrevFacingDataOffset MaterialRandomDataOffset MaterialParamDataOffset MaterialParam2DataOffset DistanceFromStartOffset V0RangeOverrideDataOffset V1RangeOverrideDataOffset OneOverInterpCount ParticleIdMask InterpIdMask ShouldFlipNormalToView U0DistributionMode SHADER_PARAMETER ( int, U1DistributionMode )

CameraRight ScreenAlignment PrevPositionDataOffset WidthDataOffset TwistDataOffset ColorDataOffset PrevFacingDataOffset MaterialRandomDataOffset MaterialParamDataOffset MaterialParam2DataOffset DistanceFromStartOffset V0RangeOverrideDataOffset V1RangeOverrideDataOffset OneOverInterpCount ParticleIdMask InterpIdMask ShouldFlipNormalToView U0DistributionMode SystemLWCTile SHADER_PARAMETER ( FVector4f, PackedVData )

NiagaraFloatDataStride SHADER_PARAMETER ( uint32, FacingMode )

NiagaraFloatDataStride Shape SHADER_PARAMETER ( uint32, NeedsPreciseMotionVectors )

NiagaraFloatDataStride Shape UseGeometryNormals SHADER_PARAMETER ( uint32, UseIndexBufferForRayTracing )

NiagaraFloatDataStride Shape UseGeometryNormals IndexBuffer TangentsAndDistances PackedPerRibbonDataByIndex NiagaraParticleDataHalf IndirectDrawOutput SHADER_PARAMETER ( int32, IndirectDrawOutputOffset )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half SHADER_PARAMETER ( FVector4f, MacroUVParameters )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset SHADER_PARAMETER ( int, PrevPositionDataOffset )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset SHADER_PARAMETER ( int, PrevVelocityDataOffset )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SHADER_PARAMETER ( int, PrevRotationDataOffset )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SHADER_PARAMETER ( int, PrevSizeDataOffset )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset SHADER_PARAMETER ( int, ColorDataOffset )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask SHADER_PARAMETER ( int, MaterialParamDataOffset )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset SHADER_PARAMETER ( int, MaterialParam2DataOffset )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset MaterialParam3DataOffset SHADER_PARAMETER ( int, FacingDataOffset )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset MaterialParam3DataOffset PrevFacingDataOffset SHADER_PARAMETER ( int, AlignmentDataOffset )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset MaterialParam3DataOffset PrevFacingDataOffset PrevAlignmentDataOffset SHADER_PARAMETER ( int, SubImageBlendMode )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset MaterialParam3DataOffset PrevFacingDataOffset PrevAlignmentDataOffset CameraOffsetDataOffset SHADER_PARAMETER ( int, PrevCameraOffsetDataOffset )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset MaterialParam3DataOffset PrevFacingDataOffset PrevAlignmentDataOffset CameraOffsetDataOffset UVScaleDataOffset SHADER_PARAMETER ( int, PivotOffsetDataOffset )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset MaterialParam3DataOffset PrevFacingDataOffset PrevAlignmentDataOffset CameraOffsetDataOffset UVScaleDataOffset PrevPivotOffsetDataOffset SHADER_PARAMETER ( int, NormalizedAgeDataOffset )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset MaterialParam3DataOffset PrevFacingDataOffset PrevAlignmentDataOffset CameraOffsetDataOffset UVScaleDataOffset PrevPivotOffsetDataOffset MaterialRandomDataOffset SHADER_PARAMETER ( FVector4f, DefaultPos )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset MaterialParam3DataOffset PrevFacingDataOffset PrevAlignmentDataOffset CameraOffsetDataOffset UVScaleDataOffset PrevPivotOffsetDataOffset MaterialRandomDataOffset DefaultPrevPos SHADER_PARAMETER ( FVector2f, DefaultSize )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset MaterialParam3DataOffset PrevFacingDataOffset PrevAlignmentDataOffset CameraOffsetDataOffset UVScaleDataOffset PrevPivotOffsetDataOffset MaterialRandomDataOffset DefaultPrevPos DefaultPrevSize SHADER_PARAMETER ( FVector2f, DefaultUVScale )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset MaterialParam3DataOffset PrevFacingDataOffset PrevAlignmentDataOffset CameraOffsetDataOffset UVScaleDataOffset PrevPivotOffsetDataOffset MaterialRandomDataOffset DefaultPrevPos DefaultPrevSize DefaultVelocity SHADER_PARAMETER ( FVector3f, DefaultPrevVelocity )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset MaterialParam3DataOffset PrevFacingDataOffset PrevAlignmentDataOffset CameraOffsetDataOffset UVScaleDataOffset PrevPivotOffsetDataOffset MaterialRandomDataOffset DefaultPrevPos DefaultPrevSize DefaultVelocity SystemLWCTile SHADER_PARAMETER ( float, DefaultRotation )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset MaterialParam3DataOffset PrevFacingDataOffset PrevAlignmentDataOffset CameraOffsetDataOffset UVScaleDataOffset PrevPivotOffsetDataOffset MaterialRandomDataOffset DefaultPrevPos DefaultPrevSize DefaultVelocity SystemLWCTile DefaultPrevRotation SHADER_PARAMETER ( FVector4f, DefaultColor )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset MaterialParam3DataOffset PrevFacingDataOffset PrevAlignmentDataOffset CameraOffsetDataOffset UVScaleDataOffset PrevPivotOffsetDataOffset MaterialRandomDataOffset DefaultPrevPos DefaultPrevSize DefaultVelocity SystemLWCTile DefaultPrevRotation DefaultMatRandom SHADER_PARAMETER ( float, DefaultCamOffset )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset MaterialParam3DataOffset PrevFacingDataOffset PrevAlignmentDataOffset CameraOffsetDataOffset UVScaleDataOffset PrevPivotOffsetDataOffset MaterialRandomDataOffset DefaultPrevPos DefaultPrevSize DefaultVelocity SystemLWCTile DefaultPrevRotation DefaultMatRandom DefaultPrevCamOffset SHADER_PARAMETER ( float, DefaultNormAge )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset MaterialParam3DataOffset PrevFacingDataOffset PrevAlignmentDataOffset CameraOffsetDataOffset UVScaleDataOffset PrevPivotOffsetDataOffset MaterialRandomDataOffset DefaultPrevPos DefaultPrevSize DefaultVelocity SystemLWCTile DefaultPrevRotation DefaultMatRandom DefaultPrevCamOffset DefaultSubImage SHADER_PARAMETER ( FVector4f, DefaultFacing )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset MaterialParam3DataOffset PrevFacingDataOffset PrevAlignmentDataOffset CameraOffsetDataOffset UVScaleDataOffset PrevPivotOffsetDataOffset MaterialRandomDataOffset DefaultPrevPos DefaultPrevSize DefaultVelocity SystemLWCTile DefaultPrevRotation DefaultMatRandom DefaultPrevCamOffset DefaultSubImage DefaultPrevFacing SHADER_PARAMETER ( FVector4f, DefaultAlignment )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset MaterialParam3DataOffset PrevFacingDataOffset PrevAlignmentDataOffset CameraOffsetDataOffset UVScaleDataOffset PrevPivotOffsetDataOffset MaterialRandomDataOffset DefaultPrevPos DefaultPrevSize DefaultVelocity SystemLWCTile DefaultPrevRotation DefaultMatRandom DefaultPrevCamOffset DefaultSubImage DefaultPrevFacing DefaultPrevAlignment SHADER_PARAMETER ( FVector4f, DefaultDynamicMaterialParameter0 )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset MaterialParam3DataOffset PrevFacingDataOffset PrevAlignmentDataOffset CameraOffsetDataOffset UVScaleDataOffset PrevPivotOffsetDataOffset MaterialRandomDataOffset DefaultPrevPos DefaultPrevSize DefaultVelocity SystemLWCTile DefaultPrevRotation DefaultMatRandom DefaultPrevCamOffset DefaultSubImage DefaultPrevFacing DefaultPrevAlignment DefaultDynamicMaterialParameter1 SHADER_PARAMETER ( FVector4f, DefaultDynamicMaterialParameter2 )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset MaterialParam3DataOffset PrevFacingDataOffset PrevAlignmentDataOffset CameraOffsetDataOffset UVScaleDataOffset PrevPivotOffsetDataOffset MaterialRandomDataOffset DefaultPrevPos DefaultPrevSize DefaultVelocity SystemLWCTile DefaultPrevRotation DefaultMatRandom DefaultPrevCamOffset DefaultSubImage DefaultPrevFacing DefaultPrevAlignment DefaultDynamicMaterialParameter1 DefaultDynamicMaterialParameter3 SHADER_PARAMETER ( int, PixelCoverageEnabled )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half PositionDataOffset VelocityDataOffset RotationDataOffset SizeDataOffset SubimageDataOffset MaterialParamValidMask MaterialParam1DataOffset MaterialParam3DataOffset PrevFacingDataOffset PrevAlignmentDataOffset CameraOffsetDataOffset UVScaleDataOffset PrevPivotOffsetDataOffset MaterialRandomDataOffset DefaultPrevPos DefaultPrevSize DefaultVelocity SystemLWCTile DefaultPrevRotation DefaultMatRandom DefaultPrevCamOffset DefaultSubImage DefaultPrevFacing DefaultPrevAlignment DefaultDynamicMaterialParameter1 DefaultDynamicMaterialParameter3 PixelCoverageColorBlend SHADER_PARAMETER ( int, AccurateMotionVectors )

CutoutParameters SHADER_PARAMETER ( uint32, NiagaraFloatDataStride )

CutoutParameters ParticleAlignmentMode SHADER_PARAMETER ( uint32, ParticleFacingMode )

CutoutParameters ParticleAlignmentMode SortedIndicesOffset SHADER_PARAMETER ( uint32, IndirectArgsOffset )

CameraRight ScreenAlignment PrevPositionDataOffset WidthDataOffset TwistDataOffset ColorDataOffset PrevFacingDataOffset MaterialRandomDataOffset MaterialParamDataOffset MaterialParam2DataOffset DistanceFromStartOffset V0RangeOverrideDataOffset V1RangeOverrideDataOffset OneOverInterpCount ParticleIdMask InterpIdMask ShouldFlipNormalToView U0DistributionMode SystemLWCTile bLocalSpace SHADER_PARAMETER_EX ( float, DeltaSeconds, EShaderPrecisionModifier::Half )

bLocalSpace SHADER_PARAMETER_EX ( FVector4f, TangentSelector, EShaderPrecisionModifier::Half )

bLocalSpace EShaderPrecisionModifier::Half SHADER_PARAMETER_EX ( FVector4f, NormalsCylinderUnitDirection, EShaderPrecisionModifier::Half )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half SHADER_PARAMETER_EX ( FVector3f, CameraFacingBlend, EShaderPrecisionModifier::Half )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half SHADER_PARAMETER_EX ( float, RotationBias, EShaderPrecisionModifier::Half )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half SHADER_PARAMETER_EX ( float, DeltaSeconds, EShaderPrecisionModifier::Half )

bLocalSpace EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half EShaderPrecisionModifier::Half SHADER_PARAMETER_EX ( FVector2f, DefaultPrevPivotOffset, EShaderPrecisionModifier::Half )

NiagaraParticleDataFloat SHADER_PARAMETER_SRV ( Buffer< float >, NiagaraParticleDataHalf )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SHADER_PARAMETER_SRV ( Buffer< uint >, SortedIndices )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset PrevCameraOffsetDataOffset DefaultRotation DefaultVelocity DefaultPrevScale DefaultPrevPosition DefaultPrevCameraOffset NIAGARAVERTEXFACTORIES_API VertexFetch_TexCoordBuffer SHADER_PARAMETER_SRV ( Buffer< float4 >, VertexFetch_PackedTangentsBuffer )

NiagaraFloatDataStride Shape UseGeometryNormals IndexBuffer SHADER_PARAMETER_SRV ( Buffer< uint >, SortedIndices )

NiagaraFloatDataStride Shape UseGeometryNormals IndexBuffer TangentsAndDistances SHADER_PARAMETER_SRV ( Buffer< uint >, MultiRibbonIndices )

NiagaraFloatDataStride Shape UseGeometryNormals IndexBuffer TangentsAndDistances PackedPerRibbonDataByIndex SHADER_PARAMETER_SRV ( Buffer< float >, NiagaraParticleDataFloat )

NiagaraFloatDataStride Shape UseGeometryNormals IndexBuffer TangentsAndDistances PackedPerRibbonDataByIndex NiagaraParticleDataHalf SHADER_PARAMETER_SRV ( Buffer< float >, SliceVertexData )

CutoutParameters ParticleAlignmentMode SortedIndicesOffset CutoutGeometry SHADER_PARAMETER_SRV ( Buffer< float >, NiagaraParticleDataFloat )

CutoutParameters ParticleAlignmentMode SortedIndicesOffset CutoutGeometry NiagaraParticleDataHalf SHADER_PARAMETER_SRV ( Buffer< uint >, SortedIndices )

NiagaraParticleDataFloat NiagaraParticleDataInt NiagaraIntDataStride SortedIndicesOffset bLocalSpace DeltaSeconds MeshScale MeshRotation bLockedAxisEnable LockedAxisSpace RotationDataOffset VelocityDataOffset PrevScaleDataOffset PrevPositionDataOffset PrevCameraOffsetDataOffset DefaultRotation DefaultVelocity DefaultPrevScale DefaultPrevPosition DefaultPrevCameraOffset NIAGARAVERTEXFACTORIES_API SHADER_PARAMETER_STRUCT_INCLUDE ( FNiagaraMeshCommonParameters, Common )



---

## Niagara

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Niagara

**Contents:**
- Niagara
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

T BarycentricInterpolate ( FVector3f BaryCoord, T V0, T V1, T V2 )

FVector4 BarycentricInterpolate ( FVector3f BaryCoord, const FVector4& V0, const FVector4& V1, const FVector4& V2 )

T BarycentricInterpolate ( float BaryX, float BaryY, float BaryZ, T V0, T V1, T V2 )

FVector4 BarycentricInterpolate ( float BaryX, float BaryY, float BaryZ, const FVector4& V0, const FVector4& V1, const FVector4& V2 )

bool EvalConditional ( ENiagaraConditionalOperator Op, const T& A, const T& B )

void FNiagaraDataInterfaceUtilities::ForEachDataInterface ( const FNiagaraSystemInstance* SystemInstance, TFunction< bool(const FNiagaraVariableBaseVariable, UNiagaraDataInterface*DataInterface)> Actio... )

void FNiagaraDataInterfaceUtilities::ForEachDataInterface ( const FNiagaraSystemInstance* SystemInstance, TFunction< bool(const FDataInterfaceUsageContext&)> Action )

void FNiagaraDataInterfaceUtilities::ForEachDataInterface ( const UNiagaraSystem* NiagaraSystem, TFunction< bool(const FDataInterfaceUsageContext&)> Action )

void FNiagaraDataInterfaceUtilities::ForEachGpuFunction ( UNiagaraDataInterface* ResolvedRuntimeDataInterface, const UNiagaraSystem* NiagaraSystem, TFunction< bool(const UNiagaraScript*, const FNiagaraDataInterfaceGeneratedFunction&)> Action )

void FNiagaraDataInterfaceUtilities::ForEachGpuFunction ( UNiagaraDataInterface* ResolvedRuntimeDataInterface, UNiagaraComponent* Component, TFunction< bool(const UNiagaraScript*, const FNiagaraDataInterfaceGeneratedFunction&)> Action )

void FNiagaraDataInterfaceUtilities::ForEachGpuFunction ( UNiagaraDataInterface* ResolvedRuntimeDataInterface, const FNiagaraSystemInstance* SystemInstance, TFunction< bool(const UNiagaraScript*, const FNiagaraDataInterfaceGeneratedFunction&)> Action )

void FNiagaraDataInterfaceUtilities::ForEachVMFunction ( UNiagaraDataInterface* ResolvedRuntimeDataInterface, const UNiagaraSystem* NiagaraSystem, TFunction< bool(const UNiagaraScript*, const FVMExternalFunctionBindingInfo&)> Action )

void FNiagaraDataInterfaceUtilities::ForEachVMFunction ( UNiagaraDataInterface* ResolvedRuntimeDataInterface, UNiagaraComponent* Component, TFunction< bool(const UNiagaraScript*, const FVMExternalFunctionBindingInfo&)> Action )

void FNiagaraDataInterfaceUtilities::ForEachVMFunction ( UNiagaraDataInterface* ResolvedRuntimeDataInterface, const FNiagaraSystemInstance* SystemInstance, TFunction< bool(const UNiagaraScript*, const FVMExternalFunctionBindingInfo&)> Action )

bool FNiagaraUtilities::AllowComputeShaders ()

bool FNiagaraUtilities::AllowComputeShaders ( EShaderPlatform ShaderPlatform )

bool FNiagaraUtilities::AllowGPUCulling ()

bool FNiagaraUtilities::AllowGPUCulling ( EShaderPlatform ShaderPlatform )

bool FNiagaraUtilities::AllowGPUParticles ()

bool FNiagaraUtilities::AllowGPUParticles ( EShaderPlatform ShaderPlatform )

bool FNiagaraUtilities::AllowGPUSorting ()

bool FNiagaraUtilities::AllowGPUSorting ( EShaderPlatform ShaderPlatform )

bool FNiagaraUtilities::AreBufferSRVsAlwaysCreated ( EShaderPlatform ShaderPlatform )

bool FNiagaraUtilities::AreTypesAssignable ( const FNiagaraTypeDefinition& FromType, const FNiagaraTypeDefinition& ToType )

EPixelFormat FNiagaraUtilities::BufferFormatToPixelFormat ( ENiagaraGpuBufferFormat NiagaraFormat )

TOptional< EPixelFormat > FNiagaraUtilities::BufferFormatToPixelFormat ( ENiagaraGpuBufferFormat NiagaraFormat, EPixelFormatCapabilities RequiredCapabilities, int NumberOfChannels )

ETextureRenderTargetFormat FNiagaraUtilities::BufferFormatToRenderTargetFormat ( ENiagaraGpuBufferFormat NiagaraFormat )

TOptional< ETextureRenderTargetFormat > FNiagaraUtilities::BufferFormatToRenderTargetFormat ( ENiagaraGpuBufferFormat NiagaraFormat, EPixelFormatCapabilities RequiredCapabilities )

ENiagaraScriptContextStaticSwitch FNiagaraUtilities::ConvertScriptUsageToStaticSwitchContext ( ENiagaraScriptUsage ScriptUsage )

ENiagaraCompileUsageStaticSwitch FNiagaraUtilities::ConvertScriptUsageToStaticSwitchUsage ( ENiagaraScriptUsage ScriptUsage )

FNiagaraVariable FNiagaraUtilities::ConvertVariableToRapidIterationConstantName ( FNiagaraVariable InVar, const TCHAR* InEmitterName, ENiagaraScriptUsage InUsage )

FString FNiagaraUtilities::CreateRapidIterationConstantName ( FName InVariableName, const TCHAR* InEmitterName, ENiagaraScriptUsage InUsage )

void FNiagaraUtilities::DumpHLSLText ( const FString& SourceCode, const FString& DebugName )

FName FNiagaraUtilities::GetUniqueName ( FName CandidateName, const TSet< FName >& ExistingNames )

bool FNiagaraUtilities::LogVerboseWarnings()

void FNiagaraUtilities::PrepareRapidIterationParameters ( const TArray< UNiagaraScript* >& Scripts, const TMap< UNiagaraScript*, UNiagaraScript* >& ScriptDependencyMap, const TMap< UNiagaraScript*, FVersionedNiagaraEmitter >& ScriptToEmitterNameMap )

FNiagaraVariable FNiagaraUtilities::ResolveAliases ( const FNiagaraVariable& InVar, const FNiagaraAliasContext& InContext )

FString FNiagaraUtilities::SanitizeNameForObjectsAndPackages ( const FString& InName )

bool FNiagaraUtilities::ShouldSyncCpuToGpu ( ENiagaraGpuSyncMode SyncMode )

bool FNiagaraUtilities::ShouldSyncGpuToCpu ( ENiagaraGpuSyncMode SyncMode )

bool FNiagaraUtilities::SupportsNiagaraRendering ( ERHIFeatureLevel::Type FeatureLevel )

bool FNiagaraUtilities::SupportsNiagaraRendering ( EShaderPlatform ShaderPlatform )

FString FNiagaraUtilities::SystemInstanceIDToString ( FNiagaraSystemInstanceID ID )

uint32 GetTypeHash ( const FNiagaraDrawIndirectArgGenTaskInfo& Info )

uint32 GetTypeHash ( const FNiagaraAssetTagDefinition& AssetTagDefinition )

uint32 GetTypeHash ( const FNiagaraDataSetID& Var )

uint32 GetTypeHash ( const FNDCMapKey& MapKey )

const FNiagaraDataSetCompiledData & NiagaraDataSetPrivate::GetCompiledData ( const FNiagaraDataSet& DataSet )

const FNiagaraDataSetCompiledData & NiagaraDataSetPrivate::GetCompiledData ( const FNiagaraDataBuffer* DataBuffer )

uint8 * NiagaraDataSetPrivate::GetComponentPtrFloat ( FNiagaraDataBuffer* DataBuffer, uint32 ComponentIdx )

const uint8 * NiagaraDataSetPrivate::GetComponentPtrFloat ( const FNiagaraDataBuffer* DataBuffer, uint32 ComponentIdx )

uint8 * NiagaraDataSetPrivate::GetComponentPtrHalf ( FNiagaraDataBuffer* DataBuffer, uint32 ComponentIdx )

const uint8 * NiagaraDataSetPrivate::GetComponentPtrHalf ( const FNiagaraDataBuffer* DataBuffer, uint32 ComponentIdx )

uint8 * NiagaraDataSetPrivate::GetComponentPtrInt32 ( FNiagaraDataBuffer* DataBuffer, uint32 ComponentIdx )

const uint8 * NiagaraDataSetPrivate::GetComponentPtrInt32 ( const FNiagaraDataBuffer* DataBuffer, uint32 ComponentIdx )

uint32 NiagaraDataSetPrivate::GetComponentStride ( const FNiagaraDataBuffer* DataBuffer )

FNiagaraDataBuffer * NiagaraDataSetPrivate::GetCurrentData ( const FNiagaraDataSet& DataSet )

FNiagaraDataBuffer * NiagaraDataSetPrivate::GetDestinationData ( const FNiagaraDataSet& DataSet )

uint32 NiagaraDataSetPrivate::GetNumInstances ( const FNiagaraDataBuffer* DataBuffer )

bool operator! ( ENiagaraAssetLibraryAssetTypes E )

bool operator! ( ENiagaraParameterBindingUsage E )

bool operator! ( ENiagaraTypeRegistryFlags E )

ENiagaraAssetLibraryAssetTypes operator& ( ENiagaraAssetLibraryAssetTypes Lhs, ENiagaraAssetLibraryAssetTypes Rhs )

ENiagaraParameterBindingUsage operator& ( ENiagaraParameterBindingUsage Lhs, ENiagaraParameterBindingUsage Rhs )

ENiagaraTypeRegistryFlags operator& ( ENiagaraTypeRegistryFlags Lhs, ENiagaraTypeRegistryFlags Rhs )

ENiagaraAssetLibraryAssetTypes & operator&= ( ENiagaraAssetLibraryAssetTypes& Lhs, ENiagaraAssetLibraryAssetTypes Rhs )

ENiagaraParameterBindingUsage & operator&= ( ENiagaraParameterBindingUsage& Lhs, ENiagaraParameterBindingUsage Rhs )

ENiagaraTypeRegistryFlags & operator&= ( ENiagaraTypeRegistryFlags& Lhs, ENiagaraTypeRegistryFlags Rhs )

ENiagaraAssetLibraryAssetTypes operator^ ( ENiagaraAssetLibraryAssetTypes Lhs, ENiagaraAssetLibraryAssetTypes Rhs )

ENiagaraParameterBindingUsage operator^ ( ENiagaraParameterBindingUsage Lhs, ENiagaraParameterBindingUsage Rhs )

ENiagaraTypeRegistryFlags operator^ ( ENiagaraTypeRegistryFlags Lhs, ENiagaraTypeRegistryFlags Rhs )

ENiagaraAssetLibraryAssetTypes & operator^= ( ENiagaraAssetLibraryAssetTypes& Lhs, ENiagaraAssetLibraryAssetTypes Rhs )

ENiagaraParameterBindingUsage & operator^= ( ENiagaraParameterBindingUsage& Lhs, ENiagaraParameterBindingUsage Rhs )

ENiagaraTypeRegistryFlags & operator^= ( ENiagaraTypeRegistryFlags& Lhs, ENiagaraTypeRegistryFlags Rhs )

ENiagaraAssetLibraryAssetTypes operator| ( ENiagaraAssetLibraryAssetTypes Lhs, ENiagaraAssetLibraryAssetTypes Rhs )

ENiagaraParameterBindingUsage operator| ( ENiagaraParameterBindingUsage Lhs, ENiagaraParameterBindingUsage Rhs )

ENiagaraTypeRegistryFlags operator| ( ENiagaraTypeRegistryFlags Lhs, ENiagaraTypeRegistryFlags Rhs )

ENiagaraAssetLibraryAssetTypes & operator|= ( ENiagaraAssetLibraryAssetTypes& Lhs, ENiagaraAssetLibraryAssetTypes Rhs )

ENiagaraParameterBindingUsage & operator|= ( ENiagaraParameterBindingUsage& Lhs, ENiagaraParameterBindingUsage Rhs )

ENiagaraTypeRegistryFlags & operator|= ( ENiagaraTypeRegistryFlags& Lhs, ENiagaraTypeRegistryFlags Rhs )

ENiagaraAssetLibraryAssetTypes operator~ ( ENiagaraAssetLibraryAssetTypes E )

ENiagaraParameterBindingUsage operator~ ( ENiagaraParameterBindingUsage E )

ENiagaraTypeRegistryFlags operator~ ( ENiagaraTypeRegistryFlags E )

FVector3f RandomBarycentricCoord ( FRandomStream& RandStream )

void SetGNiagaraDeviceProfile ( UDeviceProfile* Profile )

ENCPoolMethod ToNiagaraPooling ( EPSCPoolMethod PoolingMethod )

EPSCPoolMethod ToPSCPoolMethod ( ENCPoolMethod PoolingMethod )

UE_TRACE_CHANNEL_EXTERN ( NiagaraChannel, NIAGARA_API )



---

## NNEDenoiser

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NNEDenoiser

**Contents:**
- NNEDenoiser
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## NNERuntimeBasicCpu

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NNERuntimeBasicCpu

**Contents:**
- NNERuntimeBasicCpu
- Navigation
- Classes



---

## NNERuntimeCoreMLEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NNERuntimeCoreMLEditor

**Contents:**
- NNERuntimeCoreMLEditor
- Navigation
- Classes



---

## NNERuntimeIREEEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NNERuntimeIREEEditor

**Contents:**
- NNERuntimeIREEEditor
- Navigation
- Classes



---

## NUTUnrealEngine

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NUTUnrealEngine

**Contents:**
- NUTUnrealEngine
- Navigation
- Classes
- Interfaces



---

## NVCodecs

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NVCodecs

**Contents:**
- NVCodecs
- Navigation
- Classes
- Structs
- Functions
  - Public

DECLARE_TYPEID ( FVideoContextCUDA )

DECLARE_TYPEID ( FVideoResourceCUDA )



---

## NVDEC

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NVDEC

**Contents:**
- NVDEC
- Navigation
- Classes
- Structs
- Functions
  - Public

DECLARE_TYPEID ( FNVDEC, NVDEC_API )

DECLARE_TYPEID ( FVideoDecoderConfigNVDEC, NVDEC_API )



---

## NVENC

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/NVENC

**Contents:**
- NVENC
- Navigation
- Classes
- Structs
- Functions
  - Public

DECLARE_TYPEID ( FVideoEncoderConfigNVENC )

DECLARE_TYPEID ( FNVENC, NVENC_API )



---

## ObjectMixerEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ObjectMixerEditor

**Contents:**
- ObjectMixerEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Functions

FObjectMixerEditorListRowActor * FObjectMixerUtils::AsActorRow ( TSharedPtr< ISceneOutlinerTreeItem > InTreeItem )

FObjectMixerEditorListRowComponent * FObjectMixerUtils::AsComponentRow ( TSharedPtr< ISceneOutlinerTreeItem > InTreeItem )

FObjectMixerEditorListRowFolder * FObjectMixerUtils::AsFolderRow ( TSharedPtr< ISceneOutlinerTreeItem > InTreeItem )

FObjectMixerEditorListRowUObject * FObjectMixerUtils::AsObjectRow ( TSharedPtr< ISceneOutlinerTreeItem > InTreeItem )

FObjectMixerEditorListRowData * FObjectMixerUtils::GetRowData ( TSharedPtr< ISceneOutlinerTreeItem > InTreeItem )

UObject * FObjectMixerUtils::GetRowObject ( TSharedPtr< ISceneOutlinerTreeItem > InTreeItem, const bool bGetHybridRowComponent )

AActor * FObjectMixerUtils::GetSelfOrOuterAsActor ( TSharedPtr< ISceneOutlinerTreeItem > InTreeItem )

bool FObjectMixerUtils::IsObjectRefInCollection ( const FName& CollectionName, TSharedPtr< ISceneOutlinerTreeItem > InTreeItem )

bool FObjectMixerUtils::IsObjectRefInCollection ( const FName& CollectionName, const UObject* Object, const TSharedPtr< FObjectMixerEditorList > ListModel )

void FObjectMixerUtils::SetChildRowsSelected ( TSharedPtr< ISceneOutlinerTreeItem > InTreeItem, const bool bNewSelected, const bool bRecursive )



---

## OnlineBase

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OnlineBase

**Contents:**
- OnlineBase
- Navigation
- Classes
- Typedefs
- Enums
  - Public
- Constants
- Functions
  - Public
  - Static

const TCHAR * ELanBeaconState::ToString ( ELanBeaconState::Type EnumVal )

void GenerateNonce ( uint8* Nonce, uint32 Length )

TAutoConsoleVariable< int32 > & GetBuildIdOverrideCVar ()

TAutoConsoleVariable< int32 > & GetBuildIdOverrideCVar ()

static TAutoConsoleVariable< int32 > CVarBuildIdOverride ( TEXT("buildidoverride"), 0, TEXT("Sets build id used for matchmaking ") )



---

## OnlineBlueprintSupport

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OnlineBlueprintSupport

**Contents:**
- OnlineBlueprintSupport
- Navigation
- Classes



---

## OnlineFrameworkCommon

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OnlineFrameworkCommon

**Contents:**
- OnlineFrameworkCommon
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public



---

## OnlineServicesCommonEngineUtils

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesCommonEngineUtils

**Contents:**
- OnlineServicesCommonEngineUtils
- Navigation
- Classes



---

## OnlineServicesCommon

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesCommon

**Contents:**
- OnlineServicesCommon
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Functions

const DataType & UE::Online::GetOpDataChecked ( const TOnlineAsyncOp< OpType >& Op, const FString& Key )

uint32 UE::Online::GetTypeHash ( const FOnlineAsyncOpCache::FWrappedOperationKey& Key )

void UE::Online::LexFromString ( EOperationCacheExpirationPolicy& Value, const TCHAR*const String )

std::enable_if_t< TModels_V< Meta::COnlineMetadataAvailable, T >, bool > UE::Online::LoadConfig ( IOnlineConfigProvider& Provider, const FString& Section, T& Value )

std::enable_if_t< TModels_V< Meta::COnlineMetadataAvailable, T >, bool > UE::Online::LoadConfig ( IOnlineConfigProvider& Provider, const TArray< FString >& SectionHeirarchy, T& Value )

std::enable_if_t< TModels_V< Meta::COnlineMetadataAvailable, T >, bool > UE::Online::LoadConfig ( IOnlineConfigProvider& Provider, const FString& Section, const TCHAR* Key, T& OutValue )

std::enable_if_t< TModels_V< Meta::COnlineMetadataAvailable, T >, bool > UE::Online::LoadConfig ( IOnlineConfigProvider& Provider, const TArray< FString >& SectionHeirarchy, const TCHAR* Key, T& Value )

TUniquePtr< IOnlineExecHandler > UE::Online::MakeExecHandler ( TFunction< bool(UWorld*, const TCHAR*, FOutputDevice&)>&& Function, FString&& HelpString )

TUniquePtr< IOnlineExecHandler > UE::Online::MakeExecHandler ( T* Object, bool(T::*)(UWorld*, const TCHAR*, FOutputDevice&) Function, FString&& HelpString )

FString UE::Online::ToLogString ( const TDefaultErrorResultInternal< T >& Result )

TFuture< TArray< AwaitedType > > UE::Online::WhenAll ( TArray< TFuture< AwaitedType > >&& Futures )



---

## OnlineServicesEOSGS

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesEOSGS

**Contents:**
- OnlineServicesEOSGS
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Functions

void UE::Online::NboSerializerEOSGSSvc::SerializeFromBuffer ( FNboSerializeFromBuffer& Ar, EOnlineServices& ServicesType )

void UE::Online::NboSerializerEOSGSSvc::SerializeFromBuffer ( FNboSerializeFromBuffer& Ar, FAccountId& UniqueId )

void UE::Online::NboSerializerEOSGSSvc::SerializeFromBuffer ( FNboSerializeFromBuffer& Packet, FSessionMemberIdsSet& SessionMembersSet )

void UE::Online::NboSerializerEOSGSSvc::SerializeToBuffer ( FNboSerializeToBuffer& Ar, const EOnlineServices ServicesType )

void UE::Online::NboSerializerEOSGSSvc::SerializeToBuffer ( FNboSerializeToBuffer& Ar, const FAccountId& UniqueId )

void UE::Online::NboSerializerEOSGSSvc::SerializeToBuffer ( FNboSerializeToBuffer& Packet, const FSessionMemberIdsSet& SessionMembersSet )

bool UE::Online::ValidateOnlineId ( const TOnlineId< IdType > OnlineId )



---

## OnlineServicesEOS

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesEOS

**Contents:**
- OnlineServicesEOS
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## OnlineServicesEpicCommon

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesEpicCommon

**Contents:**
- OnlineServicesEpicCommon
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Variables
  - Public
- Functions
  - Public

bool operator!= ( const UE::Online::FOnlineError& OnlineError, EOS_EResult EosResult )

bool operator!= ( EOS_EResult EosResult, const UE::Online::FOnlineError& OnlineError )

bool operator== ( const UE::Online::FOnlineError& OnlineError, EOS_EResult EosResult )

bool operator== ( EOS_EResult EosResult, const UE::Online::FOnlineError& OnlineError )

UE::Online::Errors::UE_ONLINE_ERROR_CATEGORY ( EOS, ThirdPartyPlugin, 0x4, "EOS" )



---

## OnlineServicesInterface

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface

**Contents:**
- OnlineServicesInterface
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

TSharedRef< FUserPresence > UE::Online::ApplyPresenceMutations ( const FUserPresence& BasePresence, const FPartialUpdatePresence::Params::FMutations& Mutations )

UE::Online::ENUM_CLASS_FLAGS ( EPrivilegeResults )

ErrorCodeType UE::Online::Errors::ErrorCode::Create ( uint32 System, uint32 Category, uint32 Code )

UE::Online::Errors::LOCTEXT ( "Success", "Success" )

UE::Online::Errors::LOCTEXT ( "NotConnected", "No valid connection" )

UE::Online::Errors::LOCTEXT ( "RequestFailure", "Failed to send request" )

UE::Online::Errors::LOCTEXT ( "InvalidCreds", "Invalid credentials" )

UE::Online::Errors::LOCTEXT ( "InvalidUser", "No valid user" )

UE::Online::Errors::LOCTEXT ( "InvalidAuth", "No valid auth" )

UE::Online::Errors::LOCTEXT ( "AccessDenied", "Access denied" )

UE::Online::Errors::LOCTEXT ( "TooManyRequests", "Too many requests" )

UE::Online::Errors::LOCTEXT ( "AlreadyPending", "Request already pending" )

UE::Online::Errors::LOCTEXT ( "InvalidParams", "Invalid params specified" )

UE::Online::Errors::LOCTEXT ( "CantParse", "Cannot parse results" )

UE::Online::Errors::LOCTEXT ( "InvalidResults", "Results were invalid" )

UE::Online::Errors::LOCTEXT ( "IncompatibleVersion", "Incompatible client version" )

UE::Online::Errors::LOCTEXT ( "NotConfigured", "No valid configuration" )

UE::Online::Errors::LOCTEXT ( "NotImplemented", "Not implemented" )

UE::Online::Errors::LOCTEXT ( "MissingInterface", "Interface not found" )

UE::Online::Errors::LOCTEXT ( "Cancelled", "Operation was cancelled" )

UE::Online::Errors::LOCTEXT ( "NotLoggedIn", "User is not logged in" )

UE::Online::Errors::LOCTEXT ( "NotFound", "Request not found" )

UE::Online::Errors::LOCTEXT ( "WillRetry", "Retrying request" )

UE::Online::Errors::LOCTEXT ( "Timeout", "Operation timed out" )

UE::Online::Errors::LOCTEXT ( "InvalidState", "Invalid state" )

UE::Online::Errors::LOCTEXT ( "Unknown", "Unknown Error" )

UE::Online::Errors::LOCTEXT ( "NoChange", "No change" )

UE::Online::Errors::LOCTEXT ( "AlreadyInSession", "Player is already in session" )

UE::Online::Errors::LOCTEXT ( "NotInSession", "Player is not in any session" )

UE::Online::Errors::LOCTEXT ( "SessionJoinDenied", "Server denied session join" )

UE::Online::Errors::TEXT ( "AlreadyUnlocked" )

UE::Online::Errors::TEXT ( "AlreadyLoggedIn" )

UE::Online::Errors::TEXT ( "success" )

UE::Online::Errors::TEXT ( "no_connection" )

UE::Online::Errors::TEXT ( "request_failure" )

UE::Online::Errors::TEXT ( "invalid_creds" )

UE::Online::Errors::TEXT ( "invalid_user" )

UE::Online::Errors::TEXT ( "invalid_auth" )

UE::Online::Errors::TEXT ( "access_denied" )

UE::Online::Errors::TEXT ( "too_many_requests" )

UE::Online::Errors::TEXT ( "already_pending" )

UE::Online::Errors::TEXT ( "invalid_params" )

UE::Online::Errors::TEXT ( "cant_parse" )

UE::Online::Errors::TEXT ( "invalid_results" )

UE::Online::Errors::TEXT ( "incompatible_version" )

UE::Online::Errors::TEXT ( "not_configured" )

UE::Online::Errors::TEXT ( "not_implemented" )

UE::Online::Errors::TEXT ( "missing_interface" )

UE::Online::Errors::TEXT ( "cancelled" )

UE::Online::Errors::TEXT ( "not_logged_in" )

UE::Online::Errors::TEXT ( "not_found" )

UE::Online::Errors::TEXT ( "will_retry" )

UE::Online::Errors::TEXT ( "timeout" )

UE::Online::Errors::TEXT ( "invalid_state" )

UE::Online::Errors::TEXT ( "unknown" )

UE::Online::Errors::TEXT ( "no_change" )

UE::Online::Errors::TEXT ( "already_in_session" )

UE::Online::Errors::TEXT ( "not_in_session" )

UE::Online::Errors::TEXT ( "session_join_denied" )

UE::Online::Errors::TEXT ( "session_full" )

UE::Online::Errors::TEXT ( "CannotQueryLocalUsers" )

UE::Online::Errors::UE_ONLINE_ERROR_CATEGORY ( Achievements, Engine, 0x5, "Achievements" )

UE::Online::Errors::UE_ONLINE_ERROR_CATEGORY ( Auth, Engine, 0x4, "Auth" )

UE::Online::Errors::UE_ONLINE_ERROR_CATEGORY ( Common, Engine, 0x1, "Online Services" )

UE::Online::Errors::UE_ONLINE_ERROR_CATEGORY ( Presence, Engine, 0x3, "Presence" )

TSharedPtr< ServicesClass > UE::Online::GetServices ( FName InstanceName, FName InstanceConfigName )

uint32 UE::Online::GetTypeHash ( const FOnlineTypeName& TypeName )

bool UE::Online::IsOnlineStatus ( ELoginStatus LoginStatus )

const TCHAR * UE::Online::LexToString ( EAsyncOpState Value )

const TCHAR * UE::Online::LexToString ( ERelationship Relationship )

UE::Online::Meta::BEGIN_ONLINE_STRUCT_META ( FAccountInfo )

UE::Online::Meta::BEGIN_ONLINE_STRUCT_META ( FOffer )

UE::Online::Meta::BEGIN_ONLINE_STRUCT_META ( FLeaderboardEntry )

UE::Online::Meta::BEGIN_ONLINE_STRUCT_META ( FLobbyMember )

UE::Online::Meta::BEGIN_ONLINE_STRUCT_META ( FUserPresence )

UE::Online::Meta::BEGIN_ONLINE_STRUCT_META ( FSchemaServiceAttributeDescriptor )

UE::Online::Meta::BEGIN_ONLINE_STRUCT_META ( FFindSessionsSearchFilter )

UE::Online::Meta::BEGIN_ONLINE_STRUCT_META ( FFriend )

UE::Online::Meta::BEGIN_ONLINE_STRUCT_META ( FUserStats )

UE::Online::Meta::BEGIN_ONLINE_STRUCT_META ( FUserInfo )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FAccountInfo, PlatformUserId )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FAccountInfo, LoginStatus )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FAccountInfo, Attributes )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FExternalAuthToken, Data )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FExternalServerAuthTicket, Data )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FVerifiedAuthSession, RemoteAccountId )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FVerifiedAuthSession, CreationTime )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FOffer, Title )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FOffer, Description )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FOffer, LongDescription )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FOffer, PurchaseLimit )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FOffer, CurrencyCode )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FOffer, FormattedRegularPrice )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FOffer, RegularPrice )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FOffer, FormattedPrice )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FOffer, Price )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FOffer, PriceDecimalPoint )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FOffer, ReleaseDate )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FOffer, ExpirationDate )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FOffer, AdditionalData )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FPurchaseOffer, Quantity )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FEntitlement, EntitlementType )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FEntitlement, ProductId )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FEntitlement, bRedeemed )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FEntitlement, Quantity )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FEntitlement, AcquiredDate )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FLeaderboardEntry, Rank )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FLobbyMember, Attributes )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FLobby, OwnerAccountId )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FLobby, LocalName )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FLobby, SchemaId )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FLobby, MaxMembers )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FLobby, JoinPolicy )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FLobby, Attributes )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FLobby, Members )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FFindLobbySearchFilter, ComparisonOp )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FUserPresence, Status )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FUserPresence, Joinability )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FUserPresence, GameStatus )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FUserPresence, StatusString )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FUserPresence, RichPresenceString )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FUserPresence, PlatformType )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSchemaServiceAttributeDescriptor, SupportedTypes )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSchemaServiceAttributeDescriptor, Flags )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSchemaServiceAttributeDescriptor, MaxSize )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSchemaServiceDescriptor, AttributeIds )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSchemaAttributeDescriptor, Type )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSchemaAttributeDescriptor, Flags )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSchemaAttributeDescriptor, UpdateGroupId )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSchemaAttributeDescriptor, MaxSize )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSchemaCategoryDescriptor, ServiceDescriptorId )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSchemaDescriptor, ParentId )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSchemaDescriptor, CategoryIds )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSchemaCategoryAttributesDescriptor, CategoryId )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSchemaCategoryAttributesDescriptor, AttributeIds )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSchemaRegistryDescriptorConfig, SchemaCategoryDescriptors )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSchemaRegistryDescriptorConfig, SchemaAttributeDescriptors )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSchemaRegistryDescriptorConfig, SchemaCategoryAttributeDescriptors )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSchemaRegistryDescriptorConfig, ServiceDescriptors )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FFindSessionsSearchFilter, ComparisonOp )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FFindSessionsSearchFilter, Value )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FCustomSessionSetting, Visibility )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FCustomSessionSetting, ID )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FCustomSessionSettingUpdate, NewValue )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSessionSettings, NumMaxConnections )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSessionSettings, JoinPolicy )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSessionSettings, bAllowNewMembers )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSessionSettings, CustomSettings )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSessionInfo, SessionIdOverride )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSessionInfo, bIsLANSession )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSessionInfo, bIsDedicatedServerSession )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSessionInfo, bAllowSanctionedPlayers )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSessionInfo, bAntiCheatProtected )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSessionSettingsUpdate, NumMaxConnections )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSessionSettingsUpdate, JoinPolicy )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSessionSettingsUpdate, bAllowNewMembers )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FSessionSettingsUpdate, UpdatedCustomSettings )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FFriend, DisplayName )

UE::Online::Meta::ONLINE_STRUCT_FIELD ( FFriend, Nickname )

TField< StructType, FieldType > UE::Online::Meta::Private::MakeTField ( FieldType StructType::* Pointer, const TCHAR* Name )

void UE::Online::Meta::VisitFields ( FuncType&& Func )

void UE::Online::Meta::VisitFields ( StructType&& Object, FuncType&& Func )

void UE::Online::Meta::VisitFields ( const StructType& Object, FuncType&& Func )

bool UE::Online::operator! ( ESchemaAttributeFlags E )

bool UE::Online::operator! ( ESchemaServiceAttributeFlags E )

bool UE::Online::operator! ( ESchemaServiceAttributeSupportedTypeFlags E )

bool UE::Online::operator!= ( const FOnlineError& Lhs, const FOnlineError& Rhs )

bool UE::Online::operator!= ( const FOnlineError& OnlineError, ErrorCodeType OtherErrorCode )

bool UE::Online::operator!= ( ErrorCodeType OtherErrorCode, const FOnlineError& OnlineError )

ESchemaAttributeFlags UE::Online::operator& ( ESchemaAttributeFlags Lhs, ESchemaAttributeFlags Rhs )

ESchemaServiceAttributeFlags UE::Online::operator& ( ESchemaServiceAttributeFlags Lhs, ESchemaServiceAttributeFlags Rhs )

ESchemaServiceAttributeSupportedTypeFlags UE::Online::operator& ( ESchemaServiceAttributeSupportedTypeFlags Lhs, ESchemaServiceAttributeSupportedTypeFlags Rhs )

ESchemaAttributeFlags & UE::Online::operator&= ( ESchemaAttributeFlags& Lhs, ESchemaAttributeFlags Rhs )

ESchemaServiceAttributeFlags & UE::Online::operator&= ( ESchemaServiceAttributeFlags& Lhs, ESchemaServiceAttributeFlags Rhs )

ESchemaServiceAttributeSupportedTypeFlags & UE::Online::operator&= ( ESchemaServiceAttributeSupportedTypeFlags& Lhs, ESchemaServiceAttributeSupportedTypeFlags Rhs )

ESchemaAttributeFlags UE::Online::operator^ ( ESchemaAttributeFlags Lhs, ESchemaAttributeFlags Rhs )

ESchemaServiceAttributeFlags UE::Online::operator^ ( ESchemaServiceAttributeFlags Lhs, ESchemaServiceAttributeFlags Rhs )

ESchemaServiceAttributeSupportedTypeFlags UE::Online::operator^ ( ESchemaServiceAttributeSupportedTypeFlags Lhs, ESchemaServiceAttributeSupportedTypeFlags Rhs )

ESchemaAttributeFlags & UE::Online::operator^= ( ESchemaAttributeFlags& Lhs, ESchemaAttributeFlags Rhs )

ESchemaServiceAttributeFlags & UE::Online::operator^= ( ESchemaServiceAttributeFlags& Lhs, ESchemaServiceAttributeFlags Rhs )

ESchemaServiceAttributeSupportedTypeFlags & UE::Online::operator^= ( ESchemaServiceAttributeSupportedTypeFlags& Lhs, ESchemaServiceAttributeSupportedTypeFlags Rhs )

ESchemaAttributeFlags UE::Online::operator| ( ESchemaAttributeFlags Lhs, ESchemaAttributeFlags Rhs )

ESchemaServiceAttributeFlags UE::Online::operator| ( ESchemaServiceAttributeFlags Lhs, ESchemaServiceAttributeFlags Rhs )

ESchemaServiceAttributeSupportedTypeFlags UE::Online::operator| ( ESchemaServiceAttributeSupportedTypeFlags Lhs, ESchemaServiceAttributeSupportedTypeFlags Rhs )

ESchemaAttributeFlags & UE::Online::operator|= ( ESchemaAttributeFlags& Lhs, ESchemaAttributeFlags Rhs )

ESchemaServiceAttributeFlags & UE::Online::operator|= ( ESchemaServiceAttributeFlags& Lhs, ESchemaServiceAttributeFlags Rhs )

ESchemaServiceAttributeSupportedTypeFlags & UE::Online::operator|= ( ESchemaServiceAttributeSupportedTypeFlags& Lhs, ESchemaServiceAttributeSupportedTypeFlags Rhs )

ESchemaAttributeFlags UE::Online::operator~ ( ESchemaAttributeFlags E )

ESchemaServiceAttributeFlags UE::Online::operator~ ( ESchemaServiceAttributeFlags E )

ESchemaServiceAttributeSupportedTypeFlags UE::Online::operator~ ( ESchemaServiceAttributeSupportedTypeFlags E )

bool UE::Online::operator== ( ErrorCodeType OtherErrorCode, const FOnlineError& OnlineError )

TDelegate< DelegateSignature > UE::Online::Private::ConstructDelegate ( ObjectOrCallableType&& ObjectOrCallable, VarTypes&&... Vars )

TDelegate< DelegateSignature > UE::Online::Private::ConstructFunctionDelegate ( CallableType&& Callable, VarTypes&&... Vars )

TDelegate< DelegateSignature > UE::Online::Private::ConstructObjectDelegate ( ObjectType Object, CallableType&& Callable, VarTypes&&... Vars )

FString UE::Online::ToLogString ( const FOnlineError& Error )

FString UE::Online::ToLogString ( const TOnlineResult< T >& Result )

FString UE::Online::ToLogString ( const TSet< T >& Set )

FString UE::Online::ToLogString ( const TPair< T, U >& Pair )

FString UE::Online::ToLogString ( const TSharedPtr< T, Mode >& Ptr )

FString UE::Online::ToLogString ( const TSharedRef< T, Mode >& Ref )

FString UE::Online::ToLogString ( const TOptional< T > Optional )

FString UE::Online::ToLogString ( const TVariant< Ts... >& Variant )

FString UE::Online::ToLogString ( const FString& String )

FString UE::Online::ToLogString ( const FName& Name )

FString UE::Online::ToLogString ( const FUtf8String& Name )

FString UE::Online::ToLogString ( const FText& Text )

FString UE::Online::ToLogString ( uint8 Value )

FString UE::Online::ToLogString ( int8 Value )

FString UE::Online::ToLogString ( uint16 Value )

FString UE::Online::ToLogString ( int16 Value )

FString UE::Online::ToLogString ( uint32 Value )

FString UE::Online::ToLogString ( int32 Value )

FString UE::Online::ToLogString ( uint64 Value )

FString UE::Online::ToLogString ( int64 Value )

FString UE::Online::ToLogString ( bool Value )

FString UE::Online::ToLogString ( float Value )

FString UE::Online::ToLogString ( double Value )

FString UE::Online::ToLogString ( const T& Value )

FString UE::Online::ToLogString ( FPlatformUserId PlatformUserId )



---

## OnlineServicesNull

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesNull

**Contents:**
- OnlineServicesNull
- Navigation
- Classes
- Structs
- Typedefs
- Functions
  - Public

void UE::Online::NboSerializerNullSvc::SerializeFromBuffer ( FNboSerializeFromBuffer& Ar, FAccountId& UniqueId )

void UE::Online::NboSerializerNullSvc::SerializeFromBuffer ( FNboSerializeFromBuffer& Packet, FSessionMemberIdsSet& SessionMembersSet )

void UE::Online::NboSerializerNullSvc::SerializeFromBuffer ( FNboSerializeFromBuffer& Ar, TMap< FSchemaAttributeId, FSchemaVariant >& Map )

void UE::Online::NboSerializerNullSvc::SerializeToBuffer ( FNboSerializeToBuffer& Ar, const FAccountId& UniqueId )

void UE::Online::NboSerializerNullSvc::SerializeToBuffer ( FNboSerializeToBuffer& Packet, const FSessionMemberIdsSet& SessionMembersSet )

void UE::Online::NboSerializerNullSvc::SerializeToBuffer ( FNboSerializeToBuffer& Ar, const TMap< FSchemaAttributeId, FSchemaVariant >& Map )



---

## OnlineServicesOSSAdapter

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesOSSAdapter

**Contents:**
- OnlineServicesOSSAdapter
- Navigation
- Classes
- Structs
- Typedefs
- Constants
- Functions
  - Public

bool operator!= ( const UE::Online::FOnlineError& Left, const FOnlineErrorOss& Right )

bool operator!= ( const FOnlineErrorOss& Left, const UE::Online::FOnlineError& Right )

bool operator== ( const UE::Online::FOnlineError& Left, const FOnlineErrorOss& Right )

bool operator== ( const FOnlineErrorOss& Left, const UE::Online::FOnlineError& Right )

auto UE::Online::MakeDelegateAdapter ( TSharedRef< ComponentType > Interface, Callback&& InCallback )

auto UE::Online::MakeDelegateAdapter ( TSharedPtr< ComponentType > Interface, Callback&& InCallback )

auto UE::Online::MakeDelegateAdapter ( ComponentType* Interface, Callback&& InCallback )

auto UE::Online::MakeDelegateAdapter ( ComponentType& Interface, Callback&& InCallback )

auto UE::Online::MakeMulticastAdapter ( TSharedRef< ComponentType > Interface, DelegateType& InDelegate, Callback&& InCallback )

auto UE::Online::MakeMulticastAdapter ( TSharedPtr< ComponentType > Interface, DelegateType& InDelegate, Callback&& InCallback )

auto UE::Online::MakeMulticastAdapter ( ComponentType* Interface, DelegateType& InDelegate, Callback&& InCallback )



---

## OnlineSubsystemAmazon

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OnlineSubsystemAmazon

**Contents:**
- OnlineSubsystemAmazon
- Navigation
- Classes
- Typedefs



---

## OnlineSubsystemEOS

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OnlineSubsystemEOS

**Contents:**
- OnlineSubsystemEOS
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## OnlineSubsystemFacebook

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OnlineSubsystemFacebook

**Contents:**
- OnlineSubsystemFacebook
- Navigation
- Classes
- Typedefs



---

## OnlineSubsystemGoogle

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OnlineSubsystemGoogle

**Contents:**
- OnlineSubsystemGoogle
- Navigation
- Classes
- Typedefs



---

## OnlineSubsystemNull

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OnlineSubsystemNull

**Contents:**
- OnlineSubsystemNull
- Navigation
- Classes
- Typedefs



---

## OnlineSubsystemSteam

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OnlineSubsystemSteam

**Contents:**
- OnlineSubsystemSteam
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## OnlineSubsystemUtils

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OnlineSubsystemUtils

**Contents:**
- OnlineSubsystemUtils
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

FText EPartyReservationResult::GetDisplayString ( EPartyReservationResult::Type Response )

const TCHAR * EPartyReservationResult::ToString ( EPartyReservationResult::Type SessionType )

FText ESpectatorReservationResult::GetDisplayString ( ESpectatorReservationResult::Type Response )

const TCHAR * ESpectatorReservationResult::ToString ( ESpectatorReservationResult::Type SessionType )

EInAppPurchaseStatus PurchaseStatusFromOnlineError ( const FOnlineError& OnlineError )

const TCHAR * ToString ( EBeaconConnectionState Value )

const TCHAR * ToString ( EClientRequestType RequestType )

const TCHAR * ToString ( ESpectatorClientRequestType RequestType )



---

## OnlineSubsystem

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OnlineSubsystem

**Contents:**
- OnlineSubsystem
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

@Param Result the result of the login process | Interfaces/OnlineExternalUIInterface.h |

Id of the session for the presence update. | Interfaces/OnlinePresenceInterface.h | |

_Pragma ( "message("OnlineJsonSerializer.h is deprecated, please use the regular JSON functionality in Serial... )

void DumpNamedSession ( const FNamedOnlineSession* NamedSession )

void DumpSession ( const FOnlineSession* Session )

void DumpSessionSettings ( const FOnlineSessionSettings* SessionSettings )

bool EFriendsLists::FromString ( EFriendsLists::Type& OutEnum, const TCHAR* InString )

const TCHAR * EFriendsLists::ToString ( EFriendsLists::Type EnumVal )

EOnlineKeyValuePairDataType::Type EOnlineKeyValuePairDataType::FromString ( const FString& EnumStr )

const TCHAR * EOnlineKeyValuePairDataType::ToString ( EOnlineKeyValuePairDataType::Type EnumVal )

EOnlinePresenceState::Type EOnlinePresenceState::FromString ( const TCHAR* StringVal )

const FText EOnlinePresenceState::ToLocText ( EOnlinePresenceState::Type EnumVal )

const TCHAR * EOnlinePresenceState::ToString ( EOnlinePresenceState::Type EnumVal )

EOnlineStoreOfferDiscountType EOnlineStoreOfferDiscount::FromString ( const TCHAR*const String )

EPartyState EPartyStateFromString ( const TCHAR* Value )

FOnlineError Errors::AccessDenied()

const TCHAR * Errors::BaseNamespace()

FOnlineError Errors::InvalidParams()

FOnlineError Errors::InvalidUser()

FOnlineError Errors::MissingInterface()

FOnlineError Errors::MissingSubsystem()

FOnlineError Errors::NotConfigured()

FOnlineError Errors::ParseError()

FOnlineError Errors::RequestFailure()

FOnlineError Errors::ResultsError()

int32 GetBeaconPortFromSessionSettings ( const FOnlineSessionSettings& SessionSettings )

int32 GetBuildUniqueId()

FUniqueNetIdPtr GetFirstSignedInUser ( IOnlineIdentityPtr IdentityInt )

uint32 GetTypeHash ( const FOnlinePartyId& Value )

bool IsPlayerInSessionImpl ( IOnlineSession* SessionInt, FName SessionName, const FUniqueNetId& UniqueId )

bool IsUniqueIdLocal ( const FUniqueNetId& UniqueId )

bool IsValid ( const FOnlinePartyTypeId Id )

EJoinRequestAction JoinRequestActionFromString ( const TCHAR* Value )

void LexFromString ( TOptional< EOnlineTournamentFormat >& Format, const TCHAR*const String )

void LexFromString ( TOptional< EOnlineTournamentState >& State, const TCHAR*const String )

void LexFromString ( TOptional< EOnlineTournamentParticipantType >& State, const TCHAR*const String )

void LexFromString ( TOptional< EOnlineTournamentParticipantState >& State, const TCHAR*const String )

void LexFromString ( TOptional< EOnlineTournamentMatchState >& State, const TCHAR*const String )

void LexFromString ( EFriendInvitePolicy& Value, const TCHAR* String )

const TCHAR * LexToString ( EVoiceChatRoomState InState )

const TCHAR * LexToString ( EPurchaseTransactionState State )

const TCHAR * LexToString ( const EOnJoinSessionCompleteResult::Type Value )

const TCHAR * LexToString ( const ESessionFailure::Type Value )

FString LexToString ( const EOnlineTournamentFormat Format )

FString LexToString ( const EOnlineTournamentState State )

FString LexToString ( const EOnlineTournamentParticipantType ParticipantType )

FString LexToString ( const EOnlineTournamentParticipantState ParticipantType )

FString LexToString ( const EOnlineTournamentMatchState ParticipantType )

const TCHAR * LexToString ( EFriendInvitePolicy EnumVal )

FOnlineError OnlineFriend::Errors::AccessDenied()

const TCHAR * OnlineFriend::Errors::BaseNamespace()

FOnlineError OnlineFriend::Errors::InvalidParams()

FOnlineError OnlineFriend::Errors::InvalidResult()

FOnlineError OnlineFriend::Errors::InvalidUser()

FOnlineError OnlineFriend::Errors::MissingInterface()

FOnlineError OnlineFriend::Errors::MissingSubsystem()

FOnlineError OnlineFriend::Errors::NotConfigured()

FOnlineError OnlineFriend::Errors::ParseError()

FOnlineError OnlineFriend::Errors::RequestFailure()

FOnlineError OnlineFriend::Errors::ResultsError()

FOnlineError OnlineIdentity::Errors::AccessDenied()

const TCHAR * OnlineIdentity::Errors::BaseNamespace()

FOnlineError OnlineIdentity::Errors::Canceled()

FOnlineError OnlineIdentity::Errors::InvalidAuth()

FOnlineError OnlineIdentity::Errors::InvalidCreds()

FOnlineError OnlineIdentity::Errors::InvalidParams()

FOnlineError OnlineIdentity::Errors::InvalidResult()

FOnlineError OnlineIdentity::Errors::InvalidUser()

FOnlineError OnlineIdentity::Errors::LoginPending()

FOnlineError OnlineIdentity::Errors::MissingInterface()

FOnlineError OnlineIdentity::Errors::MissingSubsystem()

FOnlineError OnlineIdentity::Errors::NotConfigured()

FOnlineError OnlineIdentity::Errors::ParseError()

FOnlineError OnlineIdentity::Errors::PinGrantFailure()

FOnlineError OnlineIdentity::Errors::PinGrantTimeout()

FOnlineError OnlineIdentity::Errors::RequestFailure()

FOnlineError OnlineIdentity::Errors::ResultsError()

FOnlineError OnlineIdentity::Errors::UserNotFound()

FOnlineError OnlinePresence::Errors::AccessDenied()

const TCHAR * OnlinePresence::Errors::BaseNamespace()

FOnlineError OnlinePresence::Errors::InvalidParams()

FOnlineError OnlinePresence::Errors::InvalidResult()

FOnlineError OnlinePresence::Errors::InvalidUser()

FOnlineError OnlinePresence::Errors::MissingInterface()

FOnlineError OnlinePresence::Errors::MissingSubsystem()

FOnlineError OnlinePresence::Errors::NotConfigured()

FOnlineError OnlinePresence::Errors::ParseError()

FOnlineError OnlinePresence::Errors::RequestFailure()

FOnlineError OnlinePresence::Errors::ResultsError()

FOnlineError OnlinePurchase::Errors::AccessDenied()

const TCHAR * OnlinePurchase::Errors::BaseNamespace()

FOnlineError OnlinePurchase::Errors::InvalidParams()

FOnlineError OnlinePurchase::Errors::InvalidResult()

FOnlineError OnlinePurchase::Errors::InvalidUser()

FOnlineError OnlinePurchase::Errors::MissingInterface()

FOnlineError OnlinePurchase::Errors::MissingSubsystem()

FOnlineError OnlinePurchase::Errors::NotConfigured()

FOnlineError OnlinePurchase::Errors::ParseError()

FOnlineError OnlinePurchase::Errors::RequestFailure()

FOnlineError OnlinePurchase::Errors::ResultsError()

bool operator! ( EOnlineSharingCategory E )

EOnlineSharingCategory operator& ( EOnlineSharingCategory Lhs, EOnlineSharingCategory Rhs )

EOnlineSharingCategory & operator&= ( EOnlineSharingCategory& Lhs, EOnlineSharingCategory Rhs )

EOnlineSharingCategory operator^ ( EOnlineSharingCategory Lhs, EOnlineSharingCategory Rhs )

EOnlineSharingCategory & operator^= ( EOnlineSharingCategory& Lhs, EOnlineSharingCategory Rhs )

EOnlineSharingCategory operator| ( EOnlineSharingCategory Lhs, EOnlineSharingCategory Rhs )

EOnlineSharingCategory & operator|= ( EOnlineSharingCategory& Lhs, EOnlineSharingCategory Rhs )

EOnlineSharingCategory operator~ ( EOnlineSharingCategory E )

void ParseOnlineSubsystemConfigPairs ( TArrayView< const FString > InEntries, TArray< TPair< FString, FString > >& OutPairs )

PartySystemPermissions::EPermissionType PartySystemPermissionTypeFromString ( const TCHAR* Value )

FString ToDebugString ( IOnlineIdentity::EPrivilegeResults PrivilegeResult )

FString ToDebugString ( EUserPrivileges::Type UserPrivilege )

FString ToDebugString ( const FControllerPairingChangedUserInfo& ControllerPairingChangedUserInfo )

FString ToDebugString ( const FPartyConfiguration& PartyConfiguration )

FString ToDebugString ( const IOnlinePartyJoinInfo& JoinInfo )

FString ToDebugString ( const FOnlineKeyValuePairs< FString, FVariantData >& KeyValAttrs )

FString ToDebugString ( const FOnlinePartyData& PartyData )

const TCHAR * ToLogString ( EOnSessionParticipantLeftReason LeaveReason )

const TCHAR * ToString ( const EPartyState Value )

const TCHAR * ToString ( const EMemberConnectionStatus Value )

const TCHAR * ToString ( const EMemberExitedReason Value )

const TCHAR * ToString ( const EPartyInvitationRemovedReason Value )

const TCHAR * ToString ( const EPartyRequestToJoinRemovedReason Value )

const TCHAR * ToString ( const ECreatePartyCompletionResult Value )

const TCHAR * ToString ( const ESendPartyInvitationCompletionResult Value )

const TCHAR * ToString ( const EJoinPartyCompletionResult Value )

const TCHAR * ToString ( const ELeavePartyCompletionResult Value )

const TCHAR * ToString ( const EUpdateConfigCompletionResult Value )

const TCHAR * ToString ( const EKickMemberCompletionResult Value )

const TCHAR * ToString ( const EPromoteMemberCompletionResult Value )

const TCHAR * ToString ( const EInvitationResponse Value )

const TCHAR * ToString ( const ERequestToJoinPartyCompletionResult Value )

const TCHAR * ToString ( const PartySystemPermissions::EPermissionType Value )

const TCHAR * ToString ( const EJoinRequestAction Value )

const TCHAR * ToString ( EOnlineSharingCategory CategoryType )

const TCHAR * ToString ( EOnlineStatusUpdatePrivacy PrivacyType )

static IOnlineAchievementsPtr Online::GetAchievementsInterface ( const FName SubsystemName )

static IOnlineAchievementsPtr Online::GetAchievementsInterfaceChecked ( const FName SubsystemName )

static IOnlineChatPtr Online::GetChatInterface ( const FName SubsystemName )

static IOnlineChatPtr Online::GetChatInterfaceChecked ( const FName SubsystemName )

static IOnlineEntitlementsPtr Online::GetEntitlementsInterface ( const FName SubsystemName )

static IOnlineEntitlementsPtr Online::GetEntitlementsInterfaceChecked ( const FName SubsystemName )

static IOnlineEventsPtr Online::GetEventsInterface ( const FName SubsystemName )

static IOnlineEventsPtr Online::GetEventsInterfaceChecked ( const FName SubsystemName )

static IOnlineExternalUIPtr Online::GetExternalUIInterface ( const FName SubsystemName )

static IOnlineExternalUIPtr Online::GetExternalUIInterfaceChecked ( const FName SubsystemName )

static IOnlineFriendsPtr Online::GetFriendsInterface ( const FName SubsystemName )

static IOnlineFriendsPtr Online::GetFriendsInterfaceChecked ( const FName SubsystemName )

static IOnlineIdentityPtr Online::GetIdentityInterface ( const FName SubsystemName )

static IOnlineIdentityPtr Online::GetIdentityInterfaceChecked ( const FName SubsystemName )

static IOnlineLeaderboardsPtr Online::GetLeaderboardsInterface ( const FName SubsystemName )

static IOnlineLeaderboardsPtr Online::GetLeaderboardsInterfaceChecked ( const FName SubsystemName )

static IOnlinePartyPtr Online::GetPartyInterface ( const FName SubsystemName )

static IOnlinePartyPtr Online::GetPartyInterfaceChecked ( const FName SubsystemName )

static IOnlinePresencePtr Online::GetPresenceInterface ( const FName SubsystemName )

static IOnlinePresencePtr Online::GetPresenceInterfaceChecked ( const FName SubsystemName )

static IOnlinePurchasePtr Online::GetPurchaseInterface ( const FName SubsystemName )

static IOnlinePurchasePtr Online::GetPurchaseInterfaceChecked ( const FName SubsystemName )

static IOnlineSessionPtr Online::GetSessionInterface ( const FName SubsystemName )

static IOnlineSessionPtr Online::GetSessionInterfaceChecked ( const FName SubsystemName )

static IOnlineSharedCloudPtr Online::GetSharedCloudInterface ( const FName SubsystemName )

static IOnlineSharedCloudPtr Online::GetSharedCloudInterfaceChecked ( const FName SubsystemName )

static IOnlineStatsPtr Online::GetStatsInterface ( const FName SubsystemName )

static IOnlineStatsPtr Online::GetStatsInterfaceChecked ( const FName SubsystemName )

static IOnlineTimePtr Online::GetTimeInterface ( const FName SubsystemName )

static IOnlineTimePtr Online::GetTimeInterfaceChecked ( const FName SubsystemName )

static IOnlineTitleFilePtr Online::GetTitleFileInterface ( const FName SubsystemName )

static IOnlineTitleFilePtr Online::GetTitleFileInterfaceChecked ( const FName SubsystemName )

static IOnlineUserCloudPtr Online::GetUserCloudInterface ( const FName SubsystemName )

static IOnlineUserCloudPtr Online::GetUserCloudInterfaceChecked ( const FName SubsystemName )

static IOnlineUserPtr Online::GetUserInterface ( const FName SubsystemName )

static IOnlineUserPtr Online::GetUserInterfaceChecked ( const FName SubsystemName )

static IOnlineVoicePtr Online::GetVoiceInterface ( const FName SubsystemName )

static IOnlineVoicePtr Online::GetVoiceInterfaceChecked ( const FName SubsystemName )



---

## OodleNetworkHandlerComponent

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OodleNetworkHandlerComponent

**Contents:**
- OodleNetworkHandlerComponent
- Navigation
- Classes
- Structs
- Enums
  - Public
- Variables
  - Public
- Functions
  - Public

DECLARE_NETRESULT_ENUM ( EOodleNetResult )

const TCHAR * LexToString ( EOodleNetResult Enum )



---

## OpenColorIOEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OpenColorIOEditor

**Contents:**
- OpenColorIOEditor
- Navigation
- Classes
- Interfaces



---

## OpenColorIO

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OpenColorIO

**Contents:**
- OpenColorIO
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Constants
- Variables
  - Public

bool OpenColorIOBindTextureResources ( FOpenColorIOPixelShaderParameters* Parameters, const TSortedMap< int32, FTextureResource* >& InTextureResources )

FRHITexture * OpenColorIOGetMiniFontTexture()

void UpdateOpenColorIOShaderCompilingStats ( const FOpenColorIOTransformResource* InShader )



---

## OpenCVHelper

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OpenCVHelper

**Contents:**
- OpenCVHelper
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## OpenCVLensCalibration

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OpenCVLensCalibration

**Contents:**
- OpenCVLensCalibration
- Navigation
- Interfaces



---

## OpenCVLensDistortion

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OpenCVLensDistortion

**Contents:**
- OpenCVLensDistortion
- Navigation
- Classes
- Structs
- Interfaces



---

## OpenExrWrapper

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OpenExrWrapper

**Contents:**
- OpenExrWrapper
- Navigation
- Classes



---

## OpenXRAR

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OpenXRAR

**Contents:**
- OpenXRAR
- Navigation
- Structs
- Interfaces



---

## OpenXREditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OpenXREditor

**Contents:**
- OpenXREditor
- Navigation
- Interfaces



---

## OpenXREyeTracker

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OpenXREyeTracker

**Contents:**
- OpenXREyeTracker
- Navigation
- Interfaces



---

## OpenXRHandTracking

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OpenXRHandTracking

**Contents:**
- OpenXRHandTracking
- Navigation
- Classes
- Interfaces



---

## OpenXRHMD

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OpenXRHMD

**Contents:**
- OpenXRHMD
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

void EnumerateOpenXRApiLayers ( TArray< XrApiLayerProperties >& OutProperties )

void FilterActionName ( const char* InActionName, char* OutActionName )

bool InitOpenXRCore ( XrInstance Instance )

void OpenXR::AppendChainStruct ( void*& Tail, void* NewTail )

T * OpenXR::FindChainedStructByType ( void* Head, XrStructureType XRType )

const T * OpenXR::FindChainedStructByType ( const void* Head, XrStructureType XRType )

const TCHAR * OpenXRReferenceSpaceTypeToString ( XrReferenceSpaceType e )

const TCHAR * OpenXRResultToString ( XrResult e )

const TCHAR * OpenXRSessionStateToString ( XrSessionState e )

bool operator! ( EOpenXRLayerCreationFlags E )

EOpenXRLayerCreationFlags operator& ( EOpenXRLayerCreationFlags Lhs, EOpenXRLayerCreationFlags Rhs )

EOpenXRLayerCreationFlags & operator&= ( EOpenXRLayerCreationFlags& Lhs, EOpenXRLayerCreationFlags Rhs )

EOpenXRLayerCreationFlags operator^ ( EOpenXRLayerCreationFlags Lhs, EOpenXRLayerCreationFlags Rhs )

EOpenXRLayerCreationFlags & operator^= ( EOpenXRLayerCreationFlags& Lhs, EOpenXRLayerCreationFlags Rhs )

EOpenXRLayerCreationFlags operator| ( EOpenXRLayerCreationFlags Lhs, EOpenXRLayerCreationFlags Rhs )

EOpenXRLayerCreationFlags & operator|= ( EOpenXRLayerCreationFlags& Lhs, EOpenXRLayerCreationFlags Rhs )

EOpenXRLayerCreationFlags operator~ ( EOpenXRLayerCreationFlags E )

bool PreInitOpenXRCore ( PFN_xrGetInstanceProcAddr InGetProcAddr )

FIntRect ToFIntRect ( XrRect2Di Rect )

FQuat ToFQuat ( XrQuaternionf Quat )

FTimespan ToFTimespan ( XrTime Time )

FTransform ToFTransform ( XrPosef Transform, float Scale )

FVector ToFVector ( XrVector3f Vector, float Scale )

FVector2D ToFVector2D ( XrVector2f Vector, float Scale )

FVector2D ToFVector2D ( XrExtent2Df Extent, float Scale )

FVector3f ToFVector3f ( XrVector3f Vector, float Scale )

XrExtent2Df ToXrExtent2D ( FVector2D Vector, float Scale )

XrPosef ToXrPose ( FTransform Transform, float Scale )

uint32 ToXrPriority ( int32 Priority )

XrQuaternionf ToXrQuat ( FQuat Quat )

XrRect2Di ToXrRect ( FIntRect Rect )

XrTime ToXrTime ( FTimespan Time )

XrVector3f ToXrVector ( FVector Vector, float Scale )

XrVector2f ToXrVector2f ( FVector2D Vector, float Scale )



---

## OpenXRInput

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OpenXRInput

**Contents:**
- OpenXRInput
- Navigation
- Classes
- Interfaces



---

## OpenXRMsftHandInteraction

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OpenXRMsftHandInteraction

**Contents:**
- OpenXRMsftHandInteraction
- Navigation
- Classes



---

## OpenXRViveTracker

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OpenXRViveTracker

**Contents:**
- OpenXRViveTracker
- Navigation
- Interfaces



---

## OperatorStackEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OperatorStackEditor

**Contents:**
- OperatorStackEditor
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public



---

## OptimusCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OptimusCore

**Contents:**
- OptimusCore
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

ENUM_CLASS_FLAGS(EOptimusDataTypeUsageFlags) enum class EOptimusDataTypeFlags ENUM_CLASS_FLAGS ( EOptimusDataTypeFlags )

ENUM_CLASS_FLAGS ( EOptimusValueUsage )

const void Optimus::ConvertFTransformToFMatrix3x4 ( const FTransform& InTransform, FShaderValueContainerView OutShaderValue )

FMatrix44f Optimus::ConvertFTransformToFMatrix44f ( const FTransform& InTransform )

void Optimus::ConvertObjectPathToShaderFilePath ( FString& InOutPath )

bool Optimus::ConvertShaderFilePathToObjectPath ( FString& InOutPath )

bool Optimus::EvaluateExecutionDomainExpressionParseResult ( const TVariant< Expression::FExpressionObject, Expression::FParseError >& InParseResult, TWeakObjectPtr< const UOptimusComponentSource > InComponentSource, TWeakObjectPtr< const UActorComponent > InWeakComponent, TArray< int32 >& OutInvocationThreadCount )

FString Optimus::ExtractSourceValueName ( const FString& InUniqueValueName )

bool Optimus::FindMovedItemInNameArray ( const TArray< FName >& Old, const TArray< FName >& New, FName& OutSubjectName, FName& OutNextName )

T * Optimus::FindObjectInPackageOrGlobal ( const FString& InObjectPath )

FString Optimus::FormatDimensionNames ( const TArray< FName >& InNames )

FName Optimus::GenerateUniqueNameFromExistingNames ( FName InBaseName, const TArray< FName >& InExistingNames )

TArray< UClass * > Optimus::GetClassObjectsInPackage ( UPackage* InPackage )

FString Optimus::GetCookedKernelSource ( const FString& InObjectPathName, const FString& InShaderSource, const FString& InKernelName, FIntVector InGroupSize, const TCHAR* InReadNumThreadsPerInvocationFunctionName, const TCHAR* InReadThreadIndexOffsetFunctionName, bool bInIsUnifiedDispatch )

const TCHAR * Optimus::GetKernelInternalNamespaceName()

FName Optimus::GetMemberPropertyShaderName ( UScriptStruct* InStruct, const FProperty* InMemberProperty )

FName Optimus::GetSanitizedNameForHlsl ( FName InName )

FText Optimus::GetTypeDisplayName ( UScriptStruct* InStruct )

FName Optimus::GetTypeName ( const FAssetData& InStructAsset )

FName Optimus::GetTypeName ( UScriptStruct* InStruct, bool bInShouldGetUniqueNameForUserDefinedStruct )

FName Optimus::GetUniqueNameForScope ( UObject* InScopeObj, FName InName )

TVariant< bool, FText > Optimus::IsExecutionDomainUnifiedDispatchOnly ( const FString& InExpression, TWeakObjectPtr< const UOptimusComponentSource > InComponentSource )

bool Optimus::IsSkinWeightProfileAvailable ( const FSkeletalMeshLODRenderData& InLODRenderData, FName InSkinWeightProfile )

FString Optimus::MakeUniqueValueName ( const FString& InValueName, int32 InUniqueIndex )

Expression::FParseResult Optimus::ParseExecutionDomainExpression ( const FString& InExpression, TWeakObjectPtr< const UOptimusComponentSource > InComponentSource )

void Optimus::RemoveObject ( UObject* InObjectToRemove )

bool Optimus::RenameObject ( UObject* InObjectToRename, const TCHAR* InNewName, UObject* InNewOuter )

void Optimus::RequestSkinWeightProfileForDeformer ( USkeletalMeshComponent* InSkeletalMeshComponent, FName InSkinWeightProfile, TOptional< int32 > InLOD )

static bool Optimus::IsExecutionGraphType ( EOptimusNodeGraphType InGraphType )



---

## OptimusEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OptimusEditor

**Contents:**
- OptimusEditor
- Navigation
- Classes
- Interfaces



---

## OptimusSettings

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OptimusSettings

**Contents:**
- OptimusSettings
- Navigation
- Classes
- Enums
  - Public



---

## OptionalMobileFeaturesBPLibrary

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OptionalMobileFeaturesBPLibrary

**Contents:**
- OptionalMobileFeaturesBPLibrary
- Navigation
- Classes



---

## OSC

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/OSC

**Contents:**
- OSC
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## Overview of Shaders in Plugins

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-shaders-in-plugins-unreal-engine

**Contents:**
- Overview of Shaders in Plugins
- Plugin Creation Tips
- Render Thread
- Unreal Shader Files
- Shader File Preprocessing and Virtual File Path
- First Global Shader
  - Engine/Public/Platform.usf
- Shader Development Tips
- Troubleshooting
- Existing Renderer Convention

Going over creating shaders in Plugins.

Please note that this document is not a guide on how to write HLSL code or GPU efficient shaders but merely to show you how to create a new shader using the Plugin system.

Adding new shaders for use in Unreal Engine can now be achieved via the Plugin system. Creating a shader via the Plugin system allows you to quickly and easily share what you have created with the one you want. In the following document, we will take a high-level look at what needs to done to create shaders in plugins.

For additional help, you can directly look at //Engine/Plugins/Compositing/LensDistortion's Plugin.

When creating a new Plugin, you should be aware of the following things:

Use the Plugin Wizard to quickly create all of the needed files and folders for your Plugin.

Right now, it is not possible to make drastic changes, like adding a new shader model, to the Material Editor via Plugins.

Make sure you add all of your files and folder in the required location and then regenerate your Visual Studio solution files.

In your ProjectName.uplugin, make sure that the module's LoadingPhase to PostConfigInit (only for the modules that will have shader implementations) like in the following example:

As opposed to game-side API, the RHI render commands are (and should be) enqueued by a dedicated thread: the rendering thread. The game thread enqueues FIFO (first in, first out) commands through the ENQUEUE_RENDER_COMMAND to the rendering thread. The rendering thread, therefore, can be 0 or one frame behind the game thread. As a matter of CPU performance, the synchronization between them must be avoided at all cost in production runtime. To make sure your plugin's C++ function is called by the right thread, you can add multiple asserts such as check (IsInGameThread()); or check (IsInRenderingThread()); for improved threading robustness.

There are two different shader file types that you need to be aware of when developing new shaders for use in Unreal Engine. Each file has a different purpose which you will find listed below:

Unreal Shader Format (.USF)

Should be private data only

Should contain shader entry points

USF shader files, based on HLSL language, is Unreal Engine shader file format that contains the multi platform shader code. To achieve this multi platform support, the engine's shader compiler has added an extra platform-independent source file preprocessing pass before the platform-specific shader compiler (FXC, HLSLCC for GLSL cross compilation, etc.). As a result, all #define and #if are resolved at this very first preprocessing. Of course, each platform has built-in #define to know at shader preprocessing the targeted platform, such as VULKAN_PROFILE.

As same as C/C++ files, you can include usf files with #include "HelloWorld.usf," that would include the file named HelloWorld.usf stored in the same directory as the USF file you have the #include written in. To avoid multiple includes of the same file, you can add the #pragma once pre processing directive at the top of your file. For instance:

FooBarComputeShader.usf

You can also do this from a Plugin or project module's shader to include a USF file by doing either of the following:

In the engine with #include /Engine/<FilePath>, where <FilePath> is a file path relative to //Engine/Shaders/ directory;

Or another plugin with #include /Plugin/<PluginName>/<PluginFilePath>, where <PluginName> is the name of an activated Plugin, and <PluginFilePath> is a file path relative to the Plugin's Shaders/ directory. It is the responsibility of the developer to add a dependency to the correct Plugin in the .uplugin.

Global shaders inherit from the FGlobalShader in the following manner:

To have your shader compiling on all Unreal Engine platforms, you are required to include /Engine/Public/Platform.usf in all your shader files (directly or indirectly).

You can customize locally using ConsoleVariables.ini to change some settings in the renderer to accelerate iteration process when writing shaders. For example, the following Console Variables will help you get detailed debug information about what your shader is doing:

r.ShaderDevelopmentMode = 1 To get detailed logs on shader compiles and the opportunity to retry on errors.

r.DumpShaderDebugInfo = 1 To dump preprocessed shaders in the Saved folder.

Warning: leaving this on for a while will fill your hard drive with many small files and folders so make sure to disable it when you are done.

If you are having issues getting your shader to compile or show up in the Unreal Engine editor, try the following:

If you get the error Can't compile: /Plugin/<MyPluginName>/<MyFile> not found.

Make sure to check your Plugin's module's LoadingPhase is set to PostConfigInit, and that there are no typo's in the Plugin's Shaders/ directory name.

If you get the error Can't #include "/Plugin/<ParentPluginName>/<MyFile>":

Make sure to check that the parent Plugin is activated and also check your Plugin dependency as this error means you are missing a Plugin dependency in your .uplugin or .uproject.

In the renderer, we tend to have a convention on naming shader classes and shader entry point, especially with a shader domain suffix as shown in the following table:

For example, in a C++ file, the call to FLensDistortionUVGenerationVS has VS at the end signaling that it is a Vertex Shader. Inside of a USF file the void MainVS(...) ends with a VS signaling that it is going to use the Vertex Shader. When dealing with Struct's in HLSL, the struct name should start with F like FBasePassInterpolators for example.

To read more about coding standards in Unreal Engine check out the Unreal Engine Coding Standards document for more information.

The following links contain more information about developing Global Shaders inside Unreal Engine.



**Examples:**

Example 1 (json):
```json
{
              "FileVersion" : 3,
              "Version" : 1,
              "VersionName" : "1.0",
              "FriendlyName" : "Foo",
              "Description" : "Plugin to play around with shaders.",
              "Category" : "Sandbox",
              "CreatedBy" : "Epic Games, Inc.",
              "CreatedByURL" : "http://epicgames.com",
              "DocsURL" : "",
              "MarketplaceURL" : "",
              "SupportURL" : "",
              "EnabledByDefault" : false,
              "CanContainContent" : true,
              "IsBetaVersion" : false,
              "Installed" : false,
              "Modules" :
              [
                  {
                      "Name" : "Foo",
                      "Type" : "Developer",
                      "LoadingPhase" : "PostConfigInit"
                  }
              ]
          }
```

Example 2 (unknown):
```unknown
// File shared across all Plugin's shaders
          #pragma once
		
          #include "/Engine/Public/Platform.ush"
		
          // ...
```

Example 3 (unknown):
```unknown
// File containing all foobar-related functions and structures.
          #pragma once
		
          #include "FooCommon.usf"
		
          // ...
```

Example 4 (unknown):
```unknown
// Compute shader that does foobar on the GPU
		
          #include "FooCommon.usf"
          #include "FooBar.usf"
		
          // ...
```

---

## PanoramicCapture

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PanoramicCapture

**Contents:**
- PanoramicCapture
- Navigation
- Classes



---

## Paper2DEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Paper2DEditor

**Contents:**
- Paper2DEditor
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## Paper2D

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Paper2D

**Contents:**
- Paper2D
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## PaperTiledImporter

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PaperTiledImporter

**Contents:**
- PaperTiledImporter
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## ParametricSurfaceExtension

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ParametricSurfaceExtension

**Contents:**
- ParametricSurfaceExtension
- Navigation
- Classes



---

## ParametricSurface

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ParametricSurface

**Contents:**
- ParametricSurface
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Functions
  - Public

bool ParametricSurfaceUtils::AddSurfaceData ( const TCHAR* MeshFilePath, const CADLibrary::FImportParameters& InSceneParameters, const CADLibrary::FMeshParameters& InMeshParameters, const FDatasmithTessellationOptions& InCommonTessellationOptions, FDatasmithMeshElementPayload& OutMeshPayload )



---

## Party

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Party

**Contents:**
- Party
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

const TCHAR * LexToString ( ESocialPartyInviteFailureReason Type )

const TCHAR * LexToString ( ESocialSubsystem InSubsystem )

const TCHAR * LexToString ( ESocialRelationship Relationship )

const TCHAR * LexToString ( ECrossplayPreference Preference )

bool operator! ( ESocialUserStateFlags E )

ESocialUserStateFlags operator& ( ESocialUserStateFlags Lhs, ESocialUserStateFlags Rhs )

ESocialUserStateFlags & operator&= ( ESocialUserStateFlags& Lhs, ESocialUserStateFlags Rhs )

ESocialUserStateFlags operator^ ( ESocialUserStateFlags Lhs, ESocialUserStateFlags Rhs )

ESocialUserStateFlags & operator^= ( ESocialUserStateFlags& Lhs, ESocialUserStateFlags Rhs )

ESocialUserStateFlags operator| ( ESocialUserStateFlags Lhs, ESocialUserStateFlags Rhs )

ESocialUserStateFlags & operator|= ( ESocialUserStateFlags& Lhs, ESocialUserStateFlags Rhs )

ESocialUserStateFlags operator~ ( ESocialUserStateFlags E )

bool OptedOutOfCrossplay ( ECrossplayPreference InPreference )

const TCHAR * ToString ( EPartyJoinDenialReason Type )

const TCHAR * ToString ( EPartyType Type )

const TCHAR * ToString ( EApprovalAction Type )

const TCHAR * ToString ( ESocialSubsystem SocialSubsystem )



---

## PatchCheck

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PatchCheck

**Contents:**
- PatchCheck
- Navigation
- Classes
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

const TCHAR * LexToString ( EPatchCheckResult Value )



---

## PBIK

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PBIK

**Contents:**
- PBIK
- Navigation
- Classes
- Structs
- Enums
  - Public
- Constants
- Functions
  - Public
  - Static

DECLARE_CYCLE_STAT ( TEXT("PBIK Solve"), STAT_PBIK_Solve, STATGROUP_Anim )

static float PBIK::CircularEaseOut ( const float& Input )

static float PBIK::QuarticEaseOut ( const float& Input )

static float PBIK::SquaredEaseOut ( const float& Input )



---

## PCGBiomeCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PCGBiomeCore

**Contents:**
- PCGBiomeCore
- Navigation
- Classes



---

## PCGCompute

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PCGCompute

**Contents:**
- PCGCompute
- Navigation
- Classes
- Structs
- Variables
  - Public



---

## PCGEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PCGEditor

**Contents:**
- PCGEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

void FPCGEditorCommon::Helpers::DispatchEditorToast ( const FText& Text, const FText& SubText, const float Duration )

const FAssetCategoryPath FPCGEditorCommon::PCGAdvancedAssetCategoryPath ( FPCGEditorCommon::PCGAssetCategoryPath, LOCTEXT("PCGAvancedCategory", "Advanced") )

const FAssetCategoryPath FPCGEditorCommon::PCGAssetCategoryPath ( LOCTEXT("PCGCategory", "PCG") )

bool operator! ( EPCGElementType E )

EPCGElementType operator& ( EPCGElementType Lhs, EPCGElementType Rhs )

EPCGElementType & operator&= ( EPCGElementType& Lhs, EPCGElementType Rhs )

EPCGElementType operator^ ( EPCGElementType Lhs, EPCGElementType Rhs )

EPCGElementType & operator^= ( EPCGElementType& Lhs, EPCGElementType Rhs )

EPCGElementType operator| ( EPCGElementType Lhs, EPCGElementType Rhs )

EPCGElementType & operator|= ( EPCGElementType& Lhs, EPCGElementType Rhs )

EPCGElementType operator~ ( EPCGElementType E )

void PCGDataVisualizationHelpers::AddPropertyEnumColumnInfo ( FPCGTableVisualizerInfo& OutInfo, const UPCGData* Data, EnumType EnumValue, const FColumnInfoOverrides& Overrides )

void PCGDataVisualizationHelpers::AddPropertyEnumColumnInfo ( FPCGTableVisualizerInfo& OutInfo, const UPCGData* Data, const UEnum* EnumClass, int64 EnumValue, const FColumnInfoOverrides& Overrides )

void PCGDataVisualizationHelpers::AddTypedColumnInfo ( FPCGTableVisualizerInfo& OutInfo, const UPCGData* Data, const FPCGAttributePropertySelector& InSelector, const FColumnInfoOverrides& Overrides )

void PCGDataVisualizationHelpers::AddTypedColumnInfo_Impl ( FPCGTableVisualizerInfo& OutInfo, const UPCGData* Data, const FPCGAttributePropertySelector& InSelector, const FColumnInfoOverrides& Overrides )



---

## PCGExternalDataInteropEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PCGExternalDataInteropEditor

**Contents:**
- PCGExternalDataInteropEditor
- Navigation
- Classes
- Structs



---

## PCGExternalDataInterop

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PCGExternalDataInterop

**Contents:**
- PCGExternalDataInterop
- Navigation
- Classes
- Enums
  - Public



---

## PCGFastGeoInterop

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PCGFastGeoInterop

**Contents:**
- PCGFastGeoInterop
- Navigation
- Classes



---

## PCGGeometryScriptInterop

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PCGGeometryScriptInterop

**Contents:**
- PCGGeometryScriptInterop
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Constants
- Functions
  - Public

UPCGDynamicMeshManagedComponent * PCGDynamicMeshManagedComponent::GetOrCreateDynamicMeshManagedComponent ( FPCGContext* Context, const UPCGSettingsInterface* SettingsInterface, const UPCGDynamicMeshData* InMeshData, AActor* TargetActor, TOptional< EPCGEditorDirtyMode > OptionalDirtyModeOverride )

bool PCGGetDynamicMeshData::GetDynamicMeshDataFromActor ( FPCGContext*, const FPCGGetDataFunctionRegistryParams&, AActor*, FPCGGetDataFunctionRegistryOutput& )

bool PCGGetDynamicMeshData::GetDynamicMeshDataFromComponent ( FPCGContext*, const FPCGGetDataFunctionRegistryParams&, UActorComponent*, FPCGGetDataFunctionRegistryOutput& )



---

## PCGInstancedActorsInterop

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PCGInstancedActorsInterop

**Contents:**
- PCGInstancedActorsInterop
- Navigation
- Classes



---

## PCGNiagaraInterop

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PCGNiagaraInterop

**Contents:**
- PCGNiagaraInterop
- Navigation
- Classes
- Structs
- Functions
  - Public

bool PCGAttributeNiagaraTraits::AreTypesCompatible ( uint16 PCGType, const FNiagaraVariableBase& NiagaraVar, bool bPCGToNiagara )

decltype(auto) PCGAttributeNiagaraTraits::CallbackWithNiagaraType ( const FNiagaraVariableBase& NiagaraVar, Func Callback, Args&&... InArgs )



---

## PCGPythonInteropEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PCGPythonInteropEditor

**Contents:**
- PCGPythonInteropEditor
- Navigation
- Classes
- Enums
  - Public



---

## PCGWaterInterop

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PCGWaterInterop

**Contents:**
- PCGWaterInterop
- Navigation
- Classes
- Structs



---

## PCG

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PCG

**Contents:**
- PCG
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

TCopyQualifiersFromTo_T< const TObjectPtr< const UPCGData >, To > * Cast ( const FPCGDataPtrWrapper& InSrc )

TCopyQualifiersFromTo_T< const TObjectPtr< const UPCGData >, To > * CastChecked ( const FPCGDataPtrWrapper& InSrc, ECastCheckedType::Type CheckType )

DEFINE_ACTORDESC_TYPE ( APCGPartitionActor, FPCGPartitionActorDesc )

bool FPCGAsync::AsyncProcessing ( FPCGAsyncState* AsyncState, int32 NumIterations, TArray< OutputType, AllocatorType >& OutData, Func&& InFunc, const bool bEnableTimeSlicing, const int32 ChunkSize, bool bAllowChunkSizeOverride )

bool FPCGAsync::AsyncProcessingEx ( FPCGAsyncState* AsyncState, int32 NumIterations, InitializeFunc&& Initialize, ProcessElementFunc&& ProcessElement, MoveFunc&& MoveData, FinishedFunc&& Finished, const bool bEnableTimeSlicing, const int32 ChunkSize, const bool bAllowChunkSizeOverride )

bool FPCGAsync::AsyncProcessingOneToOneEx ( FPCGAsyncState* AsyncState, int32 NumIterations, InitializeFunc&& Initialize, ProcessElementFunc&& ProcessElement, const bool bEnableTimeSlicing, const int32 ChunkSize, const bool bAllowChunkSizeOverride )

bool FPCGAsync::AsyncProcessingOneToOneRangeEx ( FPCGAsyncState* AsyncState, int32 NumIterations, InitializeFunc&& Initialize, ProcessRangeFunc&& ProcessRange, const bool bEnableTimeSlicing, const int32 ChunkSize, const bool bAllowChunkSizeOverride )

bool FPCGAsync::AsyncProcessingRangeEx ( FPCGAsyncState* AsyncState, int32 NumIterations, InitializeFunc&& Initialize, ProcessRangeFunc&& ProcessRange, MoveDataRangeFunc&& MoveDataRange, FinishedFunc&& Finished, const bool bEnableTimeSlicing, const int32 ChunkSize, const bool bAllowChunkSizeOverride )

bool FPCGAsync::Private::AsyncProcessing ( FPCGAsyncState& AsyncState, int32 NumIterations, TFunctionRef< void(void)> Initialize, TFunctionRef< int32(int32, int32, int32)> IterationInnerLoop, TFunctionRef< void(int32, int32, int32)> MoveDataRange, TFunctionRef< void(int32)> Finished, const bool bInEnableTimeSlicing, const int32 InChunkSize, const bool bAllowChunkSizeOverride )

FPCGPointRef ( const FPCGPoint& InPoint, const FBox& InBoundsOverride )

void FPCGSpatialDataProcessing::SampleBasedRangeProcessing ( FPCGAsyncState* AsyncState, ProcessRangeFunc&& InProcessRange, const TArray< FPCGPoint >& SourcePoints, TArray< FPCGPoint >& OutPoints )

void FPCGSpatialDataProcessing::SampleBasedRangeProcessing ( FPCGAsyncState* AsyncState, ProcessRangeFunc&& InProcessRange, const UPCGBasePointData* SourceData, UPCGBasePointData* TargetData, EPCGPointNativeProperties PropertiesToAllocate )

uint32 GetTypeHash ( const FPCGPinReference& In )

uint32 GetTypeHash ( const FPCGISMCBuilderParameters& Key )

uint32 GetTypeHash ( const FPCGRuntimeGenerationRadii& InGenerationRadii )

uint32 GetTypeHash ( const FPCGPartitionActorRecord& In )

bool operator! ( EPCGExportMode E )

bool operator! ( EPCGComputeKernelFlags E )

bool operator! ( EPCGMetadataMathsOperation E )

bool operator! ( EPCGAttributeAccessorFlags E )

bool operator! ( EPCGSettingDefaultValueExtraFlags E )

bool operator! ( EPCGChangeType E )

bool operator! ( EPCGDataType E )

bool operator! ( EPCGHiGenGrid E )

bool operator! ( EPCGComponentDirtyFlag E )

bool operator! ( EPCGDataUsage E )

bool operator! ( EPCGPointNativeProperties E )

EPCGExportMode operator& ( EPCGExportMode Lhs, EPCGExportMode Rhs )

EPCGComputeKernelFlags operator& ( EPCGComputeKernelFlags Lhs, EPCGComputeKernelFlags Rhs )

EPCGMetadataMathsOperation operator& ( EPCGMetadataMathsOperation Lhs, EPCGMetadataMathsOperation Rhs )

EPCGAttributeAccessorFlags operator& ( EPCGAttributeAccessorFlags Lhs, EPCGAttributeAccessorFlags Rhs )

EPCGSettingDefaultValueExtraFlags operator& ( EPCGSettingDefaultValueExtraFlags Lhs, EPCGSettingDefaultValueExtraFlags Rhs )

EPCGChangeType operator& ( EPCGChangeType Lhs, EPCGChangeType Rhs )

EPCGDataType operator& ( EPCGDataType Lhs, EPCGDataType Rhs )

EPCGHiGenGrid operator& ( EPCGHiGenGrid Lhs, EPCGHiGenGrid Rhs )

EPCGComponentDirtyFlag operator& ( EPCGComponentDirtyFlag Lhs, EPCGComponentDirtyFlag Rhs )

EPCGDataUsage operator& ( EPCGDataUsage Lhs, EPCGDataUsage Rhs )

EPCGPointNativeProperties operator& ( EPCGPointNativeProperties Lhs, EPCGPointNativeProperties Rhs )

EPCGExportMode & operator&= ( EPCGExportMode& Lhs, EPCGExportMode Rhs )

EPCGComputeKernelFlags & operator&= ( EPCGComputeKernelFlags& Lhs, EPCGComputeKernelFlags Rhs )

EPCGMetadataMathsOperation & operator&= ( EPCGMetadataMathsOperation& Lhs, EPCGMetadataMathsOperation Rhs )

EPCGAttributeAccessorFlags & operator&= ( EPCGAttributeAccessorFlags& Lhs, EPCGAttributeAccessorFlags Rhs )

EPCGSettingDefaultValueExtraFlags & operator&= ( EPCGSettingDefaultValueExtraFlags& Lhs, EPCGSettingDefaultValueExtraFlags Rhs )

EPCGChangeType & operator&= ( EPCGChangeType& Lhs, EPCGChangeType Rhs )

EPCGDataType & operator&= ( EPCGDataType& Lhs, EPCGDataType Rhs )

EPCGHiGenGrid & operator&= ( EPCGHiGenGrid& Lhs, EPCGHiGenGrid Rhs )

EPCGComponentDirtyFlag & operator&= ( EPCGComponentDirtyFlag& Lhs, EPCGComponentDirtyFlag Rhs )

EPCGDataUsage & operator&= ( EPCGDataUsage& Lhs, EPCGDataUsage Rhs )

EPCGPointNativeProperties & operator&= ( EPCGPointNativeProperties& Lhs, EPCGPointNativeProperties Rhs )

EPCGExportMode operator^ ( EPCGExportMode Lhs, EPCGExportMode Rhs )

EPCGComputeKernelFlags operator^ ( EPCGComputeKernelFlags Lhs, EPCGComputeKernelFlags Rhs )

EPCGMetadataMathsOperation operator^ ( EPCGMetadataMathsOperation Lhs, EPCGMetadataMathsOperation Rhs )

EPCGAttributeAccessorFlags operator^ ( EPCGAttributeAccessorFlags Lhs, EPCGAttributeAccessorFlags Rhs )

EPCGSettingDefaultValueExtraFlags operator^ ( EPCGSettingDefaultValueExtraFlags Lhs, EPCGSettingDefaultValueExtraFlags Rhs )

EPCGChangeType operator^ ( EPCGChangeType Lhs, EPCGChangeType Rhs )

EPCGDataType operator^ ( EPCGDataType Lhs, EPCGDataType Rhs )

EPCGHiGenGrid operator^ ( EPCGHiGenGrid Lhs, EPCGHiGenGrid Rhs )

EPCGComponentDirtyFlag operator^ ( EPCGComponentDirtyFlag Lhs, EPCGComponentDirtyFlag Rhs )

EPCGDataUsage operator^ ( EPCGDataUsage Lhs, EPCGDataUsage Rhs )

EPCGPointNativeProperties operator^ ( EPCGPointNativeProperties Lhs, EPCGPointNativeProperties Rhs )

EPCGExportMode & operator^= ( EPCGExportMode& Lhs, EPCGExportMode Rhs )

EPCGComputeKernelFlags & operator^= ( EPCGComputeKernelFlags& Lhs, EPCGComputeKernelFlags Rhs )

EPCGMetadataMathsOperation & operator^= ( EPCGMetadataMathsOperation& Lhs, EPCGMetadataMathsOperation Rhs )

EPCGAttributeAccessorFlags & operator^= ( EPCGAttributeAccessorFlags& Lhs, EPCGAttributeAccessorFlags Rhs )

EPCGSettingDefaultValueExtraFlags & operator^= ( EPCGSettingDefaultValueExtraFlags& Lhs, EPCGSettingDefaultValueExtraFlags Rhs )

EPCGChangeType & operator^= ( EPCGChangeType& Lhs, EPCGChangeType Rhs )

EPCGDataType & operator^= ( EPCGDataType& Lhs, EPCGDataType Rhs )

EPCGHiGenGrid & operator^= ( EPCGHiGenGrid& Lhs, EPCGHiGenGrid Rhs )

EPCGComponentDirtyFlag & operator^= ( EPCGComponentDirtyFlag& Lhs, EPCGComponentDirtyFlag Rhs )

EPCGDataUsage & operator^= ( EPCGDataUsage& Lhs, EPCGDataUsage Rhs )

EPCGPointNativeProperties & operator^= ( EPCGPointNativeProperties& Lhs, EPCGPointNativeProperties Rhs )

EPCGExportMode operator| ( EPCGExportMode Lhs, EPCGExportMode Rhs )

EPCGComputeKernelFlags operator| ( EPCGComputeKernelFlags Lhs, EPCGComputeKernelFlags Rhs )

EPCGMetadataMathsOperation operator| ( EPCGMetadataMathsOperation Lhs, EPCGMetadataMathsOperation Rhs )

EPCGAttributeAccessorFlags operator| ( EPCGAttributeAccessorFlags Lhs, EPCGAttributeAccessorFlags Rhs )

EPCGSettingDefaultValueExtraFlags operator| ( EPCGSettingDefaultValueExtraFlags Lhs, EPCGSettingDefaultValueExtraFlags Rhs )

EPCGChangeType operator| ( EPCGChangeType Lhs, EPCGChangeType Rhs )

EPCGDataType operator| ( EPCGDataType Lhs, EPCGDataType Rhs )

EPCGHiGenGrid operator| ( EPCGHiGenGrid Lhs, EPCGHiGenGrid Rhs )

EPCGComponentDirtyFlag operator| ( EPCGComponentDirtyFlag Lhs, EPCGComponentDirtyFlag Rhs )

EPCGDataUsage operator| ( EPCGDataUsage Lhs, EPCGDataUsage Rhs )

EPCGPointNativeProperties operator| ( EPCGPointNativeProperties Lhs, EPCGPointNativeProperties Rhs )

EPCGExportMode & operator|= ( EPCGExportMode& Lhs, EPCGExportMode Rhs )

EPCGComputeKernelFlags & operator|= ( EPCGComputeKernelFlags& Lhs, EPCGComputeKernelFlags Rhs )

EPCGMetadataMathsOperation & operator|= ( EPCGMetadataMathsOperation& Lhs, EPCGMetadataMathsOperation Rhs )

EPCGAttributeAccessorFlags & operator|= ( EPCGAttributeAccessorFlags& Lhs, EPCGAttributeAccessorFlags Rhs )

EPCGSettingDefaultValueExtraFlags & operator|= ( EPCGSettingDefaultValueExtraFlags& Lhs, EPCGSettingDefaultValueExtraFlags Rhs )

EPCGChangeType & operator|= ( EPCGChangeType& Lhs, EPCGChangeType Rhs )

EPCGDataType & operator|= ( EPCGDataType& Lhs, EPCGDataType Rhs )

EPCGHiGenGrid & operator|= ( EPCGHiGenGrid& Lhs, EPCGHiGenGrid Rhs )

EPCGComponentDirtyFlag & operator|= ( EPCGComponentDirtyFlag& Lhs, EPCGComponentDirtyFlag Rhs )

EPCGDataUsage & operator|= ( EPCGDataUsage& Lhs, EPCGDataUsage Rhs )

EPCGPointNativeProperties & operator|= ( EPCGPointNativeProperties& Lhs, EPCGPointNativeProperties Rhs )

EPCGExportMode operator~ ( EPCGExportMode E )

EPCGComputeKernelFlags operator~ ( EPCGComputeKernelFlags E )

EPCGMetadataMathsOperation operator~ ( EPCGMetadataMathsOperation E )

EPCGAttributeAccessorFlags operator~ ( EPCGAttributeAccessorFlags E )

EPCGSettingDefaultValueExtraFlags operator~ ( EPCGSettingDefaultValueExtraFlags E )

EPCGChangeType operator~ ( EPCGChangeType E )

EPCGDataType operator~ ( EPCGDataType E )

EPCGHiGenGrid operator~ ( EPCGHiGenGrid E )

EPCGComponentDirtyFlag operator~ ( EPCGComponentDirtyFlag E )

EPCGDataUsage operator~ ( EPCGDataUsage E )

EPCGPointNativeProperties operator~ ( EPCGPointNativeProperties E )

bool operator== ( const FPCGISMCBuilderParameters& Other ) const

bool operator== ( const FPCGPartitionActorRecord& InOther ) const

TSharedPtr< FJsonValue > PCG::IO::Json::Helpers::ConvertFloatingPointType ( const T& Value )

void PCG::IO::Json::Helpers::SetValue ( TSharedPtr< FJsonObject >& InOutJsonObject, FString&& ValueName, const T& Value )

FString PCG::Private::GetTypeName ()

FString PCG::Private::GetTypeName ( uint16 InType )

FText PCG::Private::GetTypeNameText ()

FText PCG::Private::GetTypeNameText ( uint16 InType )

bool PCG::Private::GetValueWithBroadcast ( const InType& InValue, OutType& OutValue )

bool PCG::Private::GetValueWithBroadcastAndConstructible ( const InType& InValue, OutType& OutValue )

bool PCG::Private::IsBroadcastable ()

bool PCG::Private::IsBroadcastable ( uint16 FirstType, uint16 SecondType )

bool PCG::Private::IsBroadcastableOrConstructible ( uint16 FirstType, uint16 SecondType )

bool PCG::Private::IsConstructible ( uint16 FirstType, uint16 SecondType )

bool PCG::Private::IsMoreComplexType ()

bool PCG::Private::IsMoreComplexType ( uint16 FirstType, uint16 SecondType )

bool PCG::Private::IsOfTypes ()

bool PCG::Private::IsOfTypes ( uint16 TypeId )

bool PCG::Private::IsPCGType ()

bool PCG::Private::IsPCGType ( uint16 TypeId )

bool PCG::Private::NAryOperation::Apply ( PCGMetadataOps::FOperationData& InOperationData, int32 StartIndex, int32 Range, const Options& InOptions, const TTuple< Callbacks... >& InCallbacks, Args&&... InArgs )

bool PCG::Private::NAryOperation::Gather ( PCGMetadataOps::FOperationData& InOperationData, int32 StartIndex, int32 Range, const Options& InOptions, const TTuple< Callbacks... >& InCallbacks, int InputIndex, Signature<> S, Args&&... InArgs )

bool PCG::Private::NAryOperation::Gather ( PCGMetadataOps::FOperationData& InOperationData, int32 StartIndex, int32 Range, const Options& InOptions, const TTuple< Callbacks... >& InCallbacks, int InputIndex, Signature< InputType, InputTypes... > S, Args&&... InArgs )

bool PCG::Private::NAryOperation::Operation ( PCGMetadataOps::FOperationData& InOperationData, int32 StartIndex, int32 Range, const Options& InOptions, const TTuple< Callbacks... >& InCallbacks )

bool PCG::Private::operator! ( ESetAttributeFromTagFlags E )

ESetAttributeFromTagFlags PCG::Private::operator& ( ESetAttributeFromTagFlags Lhs, ESetAttributeFromTagFlags Rhs )

ESetAttributeFromTagFlags & PCG::Private::operator&= ( ESetAttributeFromTagFlags& Lhs, ESetAttributeFromTagFlags Rhs )

ESetAttributeFromTagFlags PCG::Private::operator^ ( ESetAttributeFromTagFlags Lhs, ESetAttributeFromTagFlags Rhs )

ESetAttributeFromTagFlags & PCG::Private::operator^= ( ESetAttributeFromTagFlags& Lhs, ESetAttributeFromTagFlags Rhs )

ESetAttributeFromTagFlags PCG::Private::operator| ( ESetAttributeFromTagFlags Lhs, ESetAttributeFromTagFlags Rhs )

ESetAttributeFromTagFlags & PCG::Private::operator|= ( ESetAttributeFromTagFlags& Lhs, ESetAttributeFromTagFlags Rhs )

ESetAttributeFromTagFlags PCG::Private::operator~ ( ESetAttributeFromTagFlags E )

void PCG::Private::Serialize ( FArchive& Ar, const T& A )

void PCG::Private::Serialize ( FArchive& Ar, T& A )

AActor * PCGActorSelector::FindActor ( const FPCGActorSelectorSettings* ActorSettings, const FPCGComponentSelectorSettings* ComponentSettings, const UPCGComponent* InComponent, const TFunction< bool(const AActor*)>& BoundsCheck, const TFunction< bool(const AActor*)>& SelfIgnoreCheck, TArrayView< AActor* > InputActors )

TUniquePtr< IPCGAttributeAccessor > PCGAttributeAccessorHelpers::CreateAccessor ( UPCGData* InData, const FPCGAttributePropertySelector& InSelector, bool bQuiet )

TUniquePtr< IPCGAttributeAccessor > PCGAttributeAccessorHelpers::CreateAccessor ( FPCGMetadataAttributeBase* InAttribute, UPCGMetadata* InMetadata, bool bQuiet )

TUniquePtr< IPCGAttributeAccessor > PCGAttributeAccessorHelpers::CreateAccessor ( FPCGMetadataAttributeBase* InAttribute, FPCGMetadataDomain* InMetadata, bool bQuiet )

TUniquePtr< IPCGAttributeAccessor > PCGAttributeAccessorHelpers::CreateAccessorWithAttributeCreation ( UPCGData* InData, const FPCGAttributePropertySelector& InSelector, const IPCGAttributeAccessor* InMatchingAccessor, EPCGAttributeAccessorFlags InTypeMatching, bool bQuiet )

TUniquePtr< const IPCGAttributeAccessor > PCGAttributeAccessorHelpers::CreateConstAccessor ( const UPCGData* InData, const FPCGAttributePropertySelector& InSelector, bool bQuiet )

TUniquePtr< const IPCGAttributeAccessor > PCGAttributeAccessorHelpers::CreateConstAccessor ( const FPCGMetadataAttributeBase* InAttribute, const UPCGMetadata* InMetadata, bool bQuiet )

TUniquePtr< const IPCGAttributeAccessor > PCGAttributeAccessorHelpers::CreateConstAccessor ( const FPCGMetadataAttributeBase* InAttribute, const FPCGMetadataDomain* InMetadata, bool bQuiet )

TUniquePtr< const IPCGAttributeAccessor > PCGAttributeAccessorHelpers::CreateConstAccessorForOverrideParamWithResult ( const FPCGDataCollection& InInputData, const FPCGSettingsOverridableParam& InParam, AccessorParamResult* OutResult )

TUniquePtr< const IPCGAttributeAccessorKeys > PCGAttributeAccessorHelpers::CreateConstKeys ( const UPCGData* InData, const FPCGAttributePropertySelector& InSelector )

TUniquePtr< IPCGAttributeAccessor > PCGAttributeAccessorHelpers::CreateExtraAccessor ( EPCGExtraProperties InExtraProperties )

TUniquePtr< IPCGAttributeAccessorKeys > PCGAttributeAccessorHelpers::CreateKeys ( UPCGData* InData, const FPCGAttributePropertySelector& InSelector )

TUniquePtr< IPCGAttributeAccessor > PCGAttributeAccessorHelpers::CreatePropertyAccessor ( const FProperty* InProperty )

TUniquePtr< IPCGAttributeAccessor > PCGAttributeAccessorHelpers::CreatePropertyAccessor ( const FName InPropertyName, const UStruct* InStruct )

TUniquePtr< IPCGAttributeAccessor > PCGAttributeAccessorHelpers::CreatePropertyChainAccessor ( TArray< const FProperty* >&& InProperties )

TUniquePtr< IPCGAttributeAccessor > PCGAttributeAccessorHelpers::CreatePropertyChainAccessor ( const TArray< FName >& InPropertyNames, const UStruct* InStruct )

bool PCGAttributeAccessorHelpers::ExtractAllValues ( const IPCGAttributeAccessor* InAccessor, const IPCGAttributeAccessorKeys* InKeys, TArray< T, AllocatorType >& OutArray, EPCGAttributeAccessorFlags GetFlags )

bool PCGAttributeAccessorHelpers::ExtractAllValues ( const UPCGData* InData, const FPCGAttributePropertyInputSelector& InSelector, TArray< T, AllocatorType >& OutArray, FPCGContext* Context, EPCGAttributeAccessorFlags GetFlags, bool bQuiet )

bool PCGAttributeAccessorHelpers::ExtractParamValue ( const UPCGData* InData, const FPCGAttributePropertyInputSelector& InSelector, T& OutValue, FPCGContext* Context, EPCGAttributeAccessorFlags GetFlags, bool bQuiet )

EPCGMetadataTypes PCGAttributeAccessorHelpers::GetMetadataTypeForProperty ( const FProperty* InProperty )

bool PCGAttributeAccessorHelpers::GetOverrideParamValue ( const IPCGAttributeAccessor& InAccessor, T& OutValue )

bool PCGAttributeAccessorHelpers::IsPropertyAccessorChainSupported ( const TArray< FName >& InPropertyNames, const UStruct* InStruct )

bool PCGAttributeAccessorHelpers::IsPropertyAccessorSupported ( const FProperty* InProperty )

bool PCGAttributeAccessorHelpers::IsPropertyAccessorSupported ( const FName InPropertyName, const UStruct* InStruct )

bool PCGAttributeAccessorHelpers::Private::DefaultStableCompareLess ( const T& A, const T& B, int32 IndexA, int32 IndexB, bool bAscending )

void PCGAttributeAccessorHelpers::SortByAttribute ( const IPCGAttributeAccessor& InAccessor, const IPCGAttributeAccessorKeys& InKeys, TArray< T >& InArray, bool bAscending, GetIndexFunc CustomGetIndex, CompareLessFunc CompareLess )

TArray< int32 > PCGAttributeAccessorHelpers::SortKeyIndicesByAttribute ( const IPCGAttributeAccessor& InAccessor, const IPCGAttributeAccessorKeys& InKeys, int32 KeyCount, bool bAscending, GetIndexFunc CustomGetIndex, CompareLessFunc CompareLess )

bool PCGAttributeAccessorHelpers::WriteAllValues ( UPCGData* OutputData, const FPCGAttributePropertyOutputSelector& OutputSelector, TArrayView< const T > InValues, const FPCGAttributePropertyInputSelector* SourceSelector, FPCGContext* Context, EPCGAttributeAccessorFlags SetFlags )

bool PCGAttributeAccessorKeys::GetKeys ( Container& InContainer, int32 InStart, TArrayView< T* > OutItems, Func&& Transform )

bool PCGAttributeAccessorKeys::IsClassSupported ( const UStruct* InClass )

bool PCGAttributeFilterHelpers::ApplyCompare ( const T& Input1, const T& Input2, EPCGAttributeFilterOperator Operation )

bool PCGAttributeFilterHelpers::ApplyRange ( const T& Input, const T& InMin, const T& InMax, bool bMinIncluded, bool bMaxIncluded )

TSet< TObjectPtr< UObject > > PCGBlueprintHelper::GetDataDependencies ( UPCGBlueprintBaseElement* InElement )

const SettingsType * PCGContextHelpers::GetInputSettings ( const UPCGNode* Node, const FPCGDataCollection& InputData )

bool PCGCopyPointsKernel::IsKernelDataValid ( const UPCGComputeKernel* InKernel, const FPCGComputeGraphContext* InContext )

bool PCGCustomAccessor::GetRange ( TArrayView< T > OutValues, int32 StartIndex, const IPCGAttributeAccessorKeys& Keys, const auto& Range )

bool PCGDataTypeCompatibilityResult::IsValid ( const EPCGDataTypeCompatibilityResult Result )

bool PCGDeterminismTests::BothDataCastsToDataType ( const UPCGData* FirstData, const UPCGData* SecondData )

bool PCGDeterminismTests::LogInvalidTest ( const UPCGNode* InPCGNode, const FName& TestName, FDeterminismTestResult& OutResult )

bool PCGDeterminismTests::MetadataAttributesAreEqual ( const FPCGMetadataAttributeBase* FirstAttributeBase, const FPCGMetadataAttributeBase* SecondAttributeBase, PCGMetadataValueKey ValueKey )

void PCGExtractAttribute::ExtractAttribute ( const FExtractAttributeParams& Params )

void PCGHelpers::ExecuteOnGameThread ( const TCHAR* DebugName, FunctorType&& Functor )

void PCGHelpers::ShiftArrayElements ( TArrayView< T > Array, int32 NumShifts )

void PCGHelpers::ShuffleArray ( FRandomStream& RandomStream, TArray< T >& Array )

KernelType * PCGKernelHelpers::CreateKernel ( FPCGGPUCompilationContext& InCompilationContext, const FCreateKernelParams& InParams, TArray< UPCGComputeKernel* >& OutKernels, TArray< FPCGKernelEdge >& OutKernelEdges )

void PCGLog::LogErrorOnGraph ( const FText& InMsg, const FPCGContext* InContext )

void PCGLog::LogWarningOnGraph ( const FText& InMsg, const FPCGContext* InContext )

void PCGLog::Metadata::LogFailToCreateAttributeError ( const FText& AttributeName, const FPCGContext* InContext )

void PCGLog::Metadata::LogFailToCreateAttributeError ( FName AttributeName, const FPCGContext* InContext )

void PCGLog::Metadata::LogFailToGetAttributeError ( const FText& AttributeName, const IPCGAttributeAccessor* Accessor, const FPCGContext* InContext )

void PCGLog::Metadata::LogFailToGetAttributeError ( FName AttributeName, const IPCGAttributeAccessor* Accessor, const FPCGContext* InContext )

void PCGLog::Metadata::LogFailToGetAttributeError ( const FPCGAttributePropertySelector& Selector, const IPCGAttributeAccessor* Accessor, const FPCGContext* InContext )

void PCGLog::Metadata::LogFailToSetAttributeError ( const FText& AttributeName, const IPCGAttributeAccessor* Accessor, const FPCGContext* InContext )

void PCGLog::Metadata::LogFailToSetAttributeError ( FName AttributeName, const IPCGAttributeAccessor* Accessor, const FPCGContext* InContext )

void PCGLog::Metadata::LogFailToSetAttributeError ( const FPCGAttributePropertySelector& Selector, const IPCGAttributeAccessor* Accessor, const FPCGContext* InContext )

FPCGMetadataAttributeBase * PCGMetadataAttribute::AllocateEmptyAttributeFromType ( int16 TypeId )

decltype(auto) PCGMetadataAttribute::CallbackWithRightType ( uint16 TypeId, Func Callback, Args&&... InArgs )

bool PCGMetadataElementCommon::ApplyOnAccessor ( const IPCGAttributeAccessorKeys& Keys, const IPCGAttributeAccessor& Accessor, Func&& InCallback, EPCGAttributeAccessorFlags Flags, const int32 ChunkSize, const int32 Count )

bool PCGMetadataElementCommon::ApplyOnAccessorRange ( const IPCGAttributeAccessorKeys& Keys, const IPCGAttributeAccessor& Accessor, Func&& Callback, EPCGAttributeAccessorFlags Flags, const int32 ChunkSize, const int32 Count )

bool PCGMetadataElementCommon::ApplyOnMultiAccessors ( const TConstArrayView< IPCGAttributeAccessorKeys const* > MultiKeys, const TConstArrayView< IPCGAttributeAccessor const* > Accessors, Func&& InCallback, EPCGAttributeAccessorFlags Flags, const int32 ChunkSize, const int32 Count )

bool PCGMetadataElementCommon::ApplyOnMultiAccessors ( const IPCGAttributeAccessorKeys& Keys, const TConstArrayView< IPCGAttributeAccessor const* > Accessors, Func&& InCallback, EPCGAttributeAccessorFlags Flags, const int32 ChunkSize, const int32 Count )

bool PCGMetadataElementCommon::ApplyOnMultiAccessorsRange ( const TConstArrayView< IPCGAttributeAccessorKeys const* > MultiKeys, const TConstArrayView< IPCGAttributeAccessor const* > Accessors, Func&& InCallback, EPCGAttributeAccessorFlags Flags, const int32 ChunkSize, const int32 Count )

bool PCGMetadataElementCommon::ApplyOnMultiAccessorsRange ( const IPCGAttributeAccessorKeys& Keys, const TConstArrayView< IPCGAttributeAccessor const* > Accessors, Func&& InCallback, EPCGAttributeAccessorFlags Flags, const int32 ChunkSize, const int32 Count )

FPCGMetadataAttribute< T > * PCGMetadataElementCommon::ClearOrCreateAttribute ( FPCGMetadataDomain* Metadata, const FName& DestinationAttribute, T DefaultValue )

FPCGMetadataAttribute< T > * PCGMetadataElementCommon::ClearOrCreateAttribute ( UPCGMetadata* Metadata, const FName& DestinationAttribute, T DefaultValue )

FPCGMetadataAttribute< T > * PCGMetadataElementCommon::ClearOrCreateAttribute ( UPCGMetadata* Metadata, const FPCGAttributePropertySelector& DestinationAttribute, T DefaultValue, FPCGContext* InOptionalContext )

TArray< FPCGPreConfiguredSettingsInfo > PCGMetadataElementCommon::FillPreconfiguredSettingsInfoFromEnum ( const TSet< EnumOperation >& InValuesToSkip, const FText& InOptionalPrefix )

bool PCGMetadataHelpers::MetadataTypeSupportsDefaultValues ( const EPCGMetadataTypes Type )

FRotator PCGMetadataRotatorHelpers::RLerp ( const FRotator& A, const FRotator& B, double Alpha, bool bShortestPath )

void PCGPointHelpers::ApplyScaleToBounds ( FTransform& InOutTransform, FVector& InOutBoundsMin, FVector& InOutBoundsMax )

FBoxSphereBounds PCGPointHelpers::GetDensityBounds ( const FTransform& InTransform, float InSteepness, const FVector& InBoundsMin, const FVector& InBoundsMax )

FVector PCGPointHelpers::GetExtents ( const FVector& InBoundsMin, const FVector& InBoundsMax )

FBox PCGPointHelpers::GetLocalBounds ( const FVector& InBoundsMin, const FVector& InBoundsMax )

FVector PCGPointHelpers::GetLocalCenter ( const FVector& InBoundsMin, const FVector& InBoundsMax )

FBox PCGPointHelpers::GetLocalDensityBounds ( float InSteepness, const FVector& InBoundsMin, const FVector& InBoundsMax )

FVector PCGPointHelpers::GetLocalSize ( const FVector& InBoundsMin, const FVector& InBoundsMax )

FVector PCGPointHelpers::GetScaledExtents ( const FTransform& InTransform, const FVector& InBoundsMin, const FVector& InBoundsMax )

FVector PCGPointHelpers::GetScaledLocalSize ( const FTransform& InTransform, const FVector& InBoundsMin, const FVector& InBoundsMax )

void PCGPointHelpers::ResetPointCenter ( const FVector& BoundsRatio, FTransform& InOutTransform, FVector& InOutBoundsMin, FVector& InOutBoundsMax )

void PCGPointHelpers::SetExtents ( const FVector& InExtents, FVector& InOutBoundsMin, FVector& InOutBoundsMax )

void PCGPointHelpers::SetLocalBounds ( const FBox& InBounds, FVector& OutBoundsMin, FVector& OutBoundsMax )

void PCGPointHelpers::SetLocalCenter ( const FVector& InCenter, FVector& InOutBoundsMin, FVector& InOutBoundsMax )

void PCGPropertyAccessor::AddressOffset ( const TArray< const FProperty* >& InProperties, TArrayView< T > InContainerKeys )

TArray< const void * > PCGPropertyAccessor::GetContainerKeys ( int32 Index, int32 Range, const IPCGAttributeAccessorKeys& Keys )

TArray< void * > PCGPropertyAccessor::GetContainerKeys ( int32 Index, int32 Range, IPCGAttributeAccessorKeys& Keys )

bool PCGPropertyAccessor::IterateGet ( const TArray< const FProperty* >& Properties, TArrayView< T >& OutValues, int32 Index, const IPCGAttributeAccessorKeys& Keys, Func&& Getter )

bool PCGPropertyAccessor::IterateSet ( const TArray< const FProperty* >& Properties, TArrayView< const T >& InValues, int32 Index, IPCGAttributeAccessorKeys& Keys, Func&& Setter )

const FName PCGPropertyHelpers::Constants::CategoryMetadataName ( "Category" )

const FName PCGPropertyHelpers::Constants::EnableCategoriesMetadataName ( "EnableCategories" )

FPropertyBagPropertyDesc PCGPropertyHelpers::CreatePropertyBagDescWithMetadataType ( FName InPropertyName, EPCGMetadataTypes Type )

TArray< T > PCGPropertyHelpers::ExtractAttributeSetAsArrayOfStructs ( const UPCGParamData* InParamData, const TMap< FName, TTuple< FName, bool > >* OptionalNameMapping, FPCGContext* OptionalContext )

UPCGParamData * PCGPropertyHelpers::ExtractPropertyAsAttributeSet ( const FExtractorParameters& Parameters, FPCGContext* OptionalContext, TSet< FSoftObjectPath >* OptionalObjectTraversed, bool bQuiet )

const FProperty * PCGPropertyHelpers::FindPropertyInUserDefinedStruct ( const UUserDefinedStruct* InStruct, const FName InName )

EPCGMetadataTypes PCGPropertyHelpers::GetMetadataTypeFromProperty ( const FProperty* InProperty )

decltype(auto) PCGPropertyHelpers::GetPropertyValueWithCallback ( const ObjectType* InObject, const FProperty* InProperty, Func InFunc )

bool PCGPropertyHelpers::SetPropertyValueFromCallback ( ObjectType* InObject, const FProperty* InProperty, Func InFunc )

bool PCGSettings::IsKeyCulled ( const TArray< FPCGSettingsAndCulling >& SettingsAndCulling )

const UPCGSpatialData * PCGSettingsHelpers::ComputeBoundingShape ( FPCGContext* Context, FName BoundingShapeLabel, bool& bOutUnionWasCreated )

bool PCGSettingsHelpers::GetOverrideValue ( const FPCGDataCollection& InInputData, const UPCGSettings* InSettings, const FName InPropertyName, const T& InDefaultValue, T& OutValue )

TArray< FPCGMarchingSquareResult > PCGSpatialAlgo::MarchingSquares ( const int32 CellCountX, const int32 CellCountY, const double Isovalue, TFunctionRef< double(int32X, int32Y)> ValueQuery, bool bUseLinearInterpolation )

PCGGrammar::FTokenizedGrammar PCGSubdivisionBase::GetTokenizedGrammar ( FPCGContext* InContext, const FString& InGrammar, const FModuleInfoMap& InModulesInfo, double& OutMinSize )

bool PCGSubdivisionBase::Subdivide ( const T& Root, double Length, TArray< TModuleInstance< T > >& OutModuleInstances, double& RemainingLength, FPCGContext* InOptionalContext, int32 InOptionalAdditionalSeed )

void PCGTestsCommon::CreateAndFillRandomAttribute ( UPCGData* InData, const FName AttributeName, T DefaultValue, const int32 NumValues, int32 Seed, const bool* bForceAllowInterpolation )

PointDataType * PCGTestsCommon::CreateEmptyPointData()

PointDataType * PCGTestsCommon::CreatePointData ()

PointDataType * PCGTestsCommon::CreatePointData ( const FVector& InLocation )

PointDataType * PCGTestsCommon::CreateRandomPointData ( int32 PointCount, int32 Seed, bool bRandomDensity )

T PCGTestsCommon::GenerateRandomValue ( FRandomStream& RandomStream )

SettingsType * PCGTestsCommon::GenerateSettings ( FTestData& TestData, TFunction< void(FTestData&)> ExtraSettingsDelegate )

static void ApplyOffset ( FPCGPointRef& InPoint )

static const bool AreElementsEqual ( const FPCGPointRef& A, const FPCGPointRef& B )

static const FBoxSphereBounds & GetBoundingBox ( const FPCGPointRef& InPoint )

static void SetElementId ( const FPCGPointRef& Element, FOctreeElementId2 OctreeElementID )



---

## PerforceSourceControl

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PerforceSourceControl

**Contents:**
- PerforceSourceControl
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## PerformanceCaptureCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PerformanceCaptureCore

**Contents:**
- PerformanceCaptureCore
- Navigation
- Classes



---

## PerformanceCaptureWorkflowRuntime

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PerformanceCaptureWorkflowRuntim-

**Contents:**
- PerformanceCaptureWorkflowRuntime
- Navigation
- Classes



---

## PerformanceCaptureWorkflow

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PerformanceCaptureWorkflow

**Contents:**
- PerformanceCaptureWorkflow
- Navigation
- Classes



---

## PFMExporter

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PFMExporter

**Contents:**
- PFMExporter
- Navigation
- Classes
- Interfaces



---

## PhysicsControlEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PhysicsControlEditor

**Contents:**
- PhysicsControlEditor
- Navigation
- Classes
- Typedefs
- Variables
  - Public
- Functions
  - Public

bool IsEqual ( const TSharedPtr< OperatorTreeItem > Lhs, const TSharedPtr< OperatorTreeItem > Rhs )

bool MatchSearchText ( const FString& TextToSearch, const TArray< TArray< FString > >& StructuredSearchCriteria )

bool operator== ( const OperatorTreeControlItem& Lhs, const OperatorTreeControlItem& Rhs )

bool operator== ( const OperatorTreeNodeItem& Lhs, const OperatorTreeNodeItem& Rhs )

bool operator== ( const OperatorTreeMessageItem& Lhs, const OperatorTreeMessageItem& Rhs )

TSharedPtr< DerivedType > StaticCastOperatorItemPtr ( const TSharedPtr< OperatorTreeItem > InItem )



---

## PhysicsControlUncookedOnly

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PhysicsControlUncookedOnly

**Contents:**
- PhysicsControlUncookedOnly
- Navigation
- Classes
- Interfaces



---

## PhysicsControl

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PhysicsControl

**Contents:**
- PhysicsControl
- Navigation
- Classes
- Structs
- Enums
  - Public
- Variables
  - Public
- Functions
  - Public

ImmediatePhysics::FJointHandle * CreatePhysicsJoint ( ImmediatePhysics::FSimulation* Simulation, ImmediatePhysics::FActorHandle* ChildActorHandle, ImmediatePhysics::FActorHandle* ParentActorHandle )

TArray< FName > ExpandName ( const FName InName, const TMap< FName, TArray< FName > >& Sets )

TArray< FName > ExpandNames ( const TArray< FName >& InNames, const TMap< FName, TArray< FName > >& Sets )

FName GetPhysicsControlTypeName ( const EPhysicsControlType ControlType )

FName GetPhysicsMovementTypeName ( const EPhysicsMovementType MovementType )

FPhysicsControlData Interpolate ( const FPhysicsControlData& A, const FPhysicsControlData& B, const float Weight )

FPhysicsControlSparseData Interpolate ( const FPhysicsControlSparseData& A, const FPhysicsControlSparseData& B, const float Weight )

FPhysicsControlModifierData Interpolate ( const FPhysicsControlModifierData& A, const FPhysicsControlModifierData& B, const float Weight )

FPhysicsControlModifierSparseData Interpolate ( const FPhysicsControlModifierSparseData& A, const FPhysicsControlModifierSparseData& B, const float Weight )

void SetPhysicsJointEnabled ( ImmediatePhysics::FJointHandle*const JointHandle, const bool bIsEnabled )

FVector UE::PhysicsControl::CalculateAngularVelocity ( const FQuat& PrevQ, const FQuat& CurrentQ, float Dt )

FVector UE::PhysicsControl::CalculateLinearVelocity ( const FVector& PrevP, const FVector& CurrentP, float Dt )

void UE::PhysicsControl::ConvertSpringToStrengthParams ( TOut& OutStrength, TOut& OutDampingRatio, TOut& OutExtraDamping, const double InSpring, const double InDamping )

void UE::PhysicsControl::ConvertStrengthToSpringParams ( TOut& OutSpring, TOut& OutDamping, double InStrength, double InDampingRatio, double InExtraDamping )

bool UE::PhysicsControl::DoesNameExist ( const FName Name, const TArray< FName >& ExistingNames )

bool UE::PhysicsControl::DoesNameExist ( const FName Name, const TMap< FName, T >& ExistingNames )

bool UE::PhysicsControl::DoesNameExist ( const FName Name, const TSet< FName >& ExistingNames )

FName UE::PhysicsControl::GetUniqueBodyModifierName ( const FName BodyName, const CollectionType& ExistingNames, const FString& NamePrefix )

FName UE::PhysicsControl::GetUniqueControlName ( const FName ParentBodyName, const FName ChildBodyName, const CollectionType& ExistingNames, const FString& NamePrefix )

FName UE::PhysicsControl::GetUniqueName ( const FString& NameBase, const CollectionType& ExistingNames, const int32 MaxNameIndex )

void UpdateBodyFromModifierData ( ImmediatePhysics::FActorHandle* ActorHandle, ImmediatePhysics::FSimulation* PhysicsSimulation, const FPhysicsControlModifierData& ModifierData, const FVector& SimSpaceGravity )

bool UpdateDriveSpringDamperSettings ( ImmediatePhysics::FJointHandle* JointHandle, const Chaos::FPBDJointSettings& Settings, const FPhysicsControlData& Data, const FPhysicsControlMultiplier& Multiplier )



---

## PixelCaptureShaders

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PixelCaptureShaders

**Contents:**
- PixelCaptureShaders
- Navigation
- Classes
- Structs



---

## PixelCapture

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PixelCapture

**Contents:**
- PixelCapture
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Constants



---

## PixelStreaming2Core

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PixelStreaming2Core

**Contents:**
- PixelStreaming2Core
- Navigation
- Classes
- Interfaces



---

## PixelStreaming2Editor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PixelStreaming2Editor

**Contents:**
- PixelStreaming2Editor
- Navigation
- Interfaces



---

## PixelStreaming2HMD

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PixelStreaming2HMD

**Contents:**
- PixelStreaming2HMD
- Navigation
- Interfaces
- Enums
  - Public



---

## PixelStreaming2Input

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PixelStreaming2Input

**Contents:**
- PixelStreaming2Input
- Navigation
- Interfaces
- Enums
  - Public



---

## PixelStreaming2RTC

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PixelStreaming2RTC

**Contents:**
- PixelStreaming2RTC
- Navigation
- Interfaces



---

## PixelStreaming2Servers

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PixelStreaming2Servers

**Contents:**
- PixelStreaming2Servers
- Navigation
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## PixelStreaming2Settings

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PixelStreaming2Settings

**Contents:**
- PixelStreaming2Settings
- Navigation
- Enums
  - Public



---

## PixelStreaming2

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PixelStreaming2

**Contents:**
- PixelStreaming2
- Navigation
- Classes
- Interfaces



---

## PixelStreamingEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PixelStreamingEditor

**Contents:**
- PixelStreamingEditor
- Navigation
- Classes
- Interfaces
- Enums
  - Public



---

## PixelStreamingHMD

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PixelStreamingHMD

**Contents:**
- PixelStreamingHMD
- Navigation
- Classes
- Interfaces
- Enums
  - Public



---

## PixelStreamingInput

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PixelStreamingInput

**Contents:**
- PixelStreamingInput
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## PixelStreamingPlayer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PixelStreamingPlayer

**Contents:**
- PixelStreamingPlayer
- Navigation
- Classes
- Structs
- Functions
  - Public

DECLARE_DYNAMIC_MULTICAST_SPARSE_DELEGATE ( FPixelStreamingOnIceDisconnection, UPixelStreamingPeerComponent, OnIceDisconnection )

DECLARE_DYNAMIC_MULTICAST_SPARSE_DELEGATE ( FPixelStreamingSignallingComponentConnected, UPixelStreamingSignallingComponent, OnConnected )

DECLARE_DYNAMIC_MULTICAST_SPARSE_DELEGATE_OneParam ( FPixelStreamingOnIceCandidate, UPixelStreamingPeerComponent, OnIceCandidate, FPixelStreamingIceCandidateWrapper, Candidate )

DECLARE_DYNAMIC_MULTICAST_SPARSE_DELEGATE_OneParam ( FPixelStreamingOnIceConnection, UPixelStreamingPeerComponent, OnIceConnection, int, Number )

DECLARE_DYNAMIC_MULTICAST_SPARSE_DELEGATE_OneParam ( FPixelStreamingSignallingComponentConnectionError, UPixelStreamingSignallingComponent, OnConnectionError, const FString&, ErrorMsg )

DECLARE_DYNAMIC_MULTICAST_SPARSE_DELEGATE_OneParam ( FPixelStreamingSignallingComponentConfig, UPixelStreamingSignallingComponent, OnConfig, FPixelStreamingRTCConfigWrapper, Config )

DECLARE_DYNAMIC_MULTICAST_SPARSE_DELEGATE_OneParam ( FPixelStreamingSignallingComponentOffer, UPixelStreamingSignallingComponent, OnOffer, const FString&, Offer )

DECLARE_DYNAMIC_MULTICAST_SPARSE_DELEGATE_OneParam ( FPixelStreamingSignallingComponentAnswer, UPixelStreamingSignallingComponent, OnAnswer, const FString&, Answer )

DECLARE_DYNAMIC_MULTICAST_SPARSE_DELEGATE_OneParam ( FPixelStreamingSignallingComponentIceCandidate, UPixelStreamingSignallingComponent, OnIceCandidate, FPixelStreamingIceCandidateWrapper, Candidate )

DECLARE_DYNAMIC_MULTICAST_SPARSE_DELEGATE_ThreeParams ( FPixelStreamingSignallingComponentDisconnected, UPixelStreamingSignallingComponent, OnDisconnected, int32, StatusCode, const FString&, Reason, bool, bWasClean )

DECLARE_DYNAMIC_MULTICAST_SPARSE_DELEGATE_TwoParams ( FPixelStreamingSignallingComponentDataChannels, UPixelStreamingSignallingComponent, OnDataChannels, int32, SendStreamId, int32, RecvStreamId )



---

## PixelStreamingServers

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PixelStreamingServers

**Contents:**
- PixelStreamingServers
- Navigation
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## PixelStreaming

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PixelStreaming

**Contents:**
- PixelStreaming
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

int32 PlayerIdToInt ( FPixelStreamingPlayerId PlayerId )

FPixelStreamingPlayerId ToPlayerId ( FString PlayerIdString )

FPixelStreamingPlayerId ToPlayerId ( int32 PlayerIdInteger )

const void * UE::PixelStreaming::ValueLoc ( T&& Value )

const void * UE::PixelStreaming::ValueLoc ( FString&& Value )

size_t UE::PixelStreaming::ValueSize ( T&& Value )

size_t UE::PixelStreaming::ValueSize ( FString&& Value )

UE_TRACE_CHANNEL_EXTERN ( PixelStreamingChannel, PIXELSTREAMING_API )



---

## PixWinPlugin

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PixWinPlugin

**Contents:**
- PixWinPlugin
- Navigation
- Interfaces



---

## PlainPropsEngine

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PlainPropsEngine

**Contents:**
- PlainPropsEngine
- Navigation
- Classes



---

## PlainPropsUObject

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PlainPropsUObject

**Contents:**
- PlainPropsUObject
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Functions
  - Public

PlainProps::UE::ENUM_CLASS_FLAGS ( ERoundtrip )



---

## PlainProps

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PlainProps

**Contents:**
- PlainProps
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Constants
- Variables
  - Public

TTuple_Ctti< Ts... > CttiOfPtr ( TTuple< Ts... >* )

FEmptyVariantState_Ctti CttiOfPtr ( FEmptyVariantState* )

void * operator new ( std::size_t Size, PlainProps::FScratchAllocator& Scratch )

void * operator new ( std::size_t Size, std::align_val_t Align, PlainProps::FScratchAllocator& Scratch )

const T * PlainProps::AlignPtr ( const void* Ptr )

void PlainProps::AppendString ( FUtf8StringBuilderBase& Out, const NameType& Str )

void PlainProps::AppendString ( FUtf8StringBuilderBase& Out, const UE::FSensitiveName& Name )

FBothStructId PlainProps::BindCustomStructOnce()

FMemberBindType PlainProps::BindInnerLeaf ( FOptionalInnerId& OutId, FMemberSpec& OutSpec, FUnpackedLeafType Leaf, FOptionalEnumId Id )

FMemberBindType PlainProps::BindInnermostType ( FOptionalInnerId& OutBindId, FMemberSpec& OutSpec )

FMemberBindType PlainProps::BindInnerStruct ( FOptionalInnerId& OutBindId, FMemberSpec& OutSpec, FBothStructId Both )

FMemberBinding PlainProps::BindMember ( uint64 Offset, FMemberSpec& OutSpec )

void PlainProps::BindNativeStruct ( FSchemaBindings& Out, FBothStructId Both, EMemberPresence Occupancy )

FTypedRange PlainProps::BuildEnumRange ( FScratchAllocator& Scratch, FEnumId Enum, TConstArrayView< T, SizeType > Values )

FTypedRange PlainProps::BuildEnumRange ( FScratchAllocator& Scratch, FEnumId Enum, ESizeType SizeType, TConstArrayView< T > Values )

FTypedRange PlainProps::BuildLeafRange ( FScratchAllocator& Scratch, TConstArrayView< T, SizeType > Values )

FTypedRange PlainProps::BuildLeafRange ( FScratchAllocator& Scratch, const T* Values, SizeType Num )

FTypedRange PlainProps::BuildLeafRange ( FScratchAllocator& Scratch, ESizeType SizeType, TConstArrayView< T > Values )

FTypedRange PlainProps::BuildLeafRange ( FScratchAllocator& Scratch, ESizeType SizeType, const T* Values, uint64 Num )

uint32 PlainProps::CountRangeBindings()

FEnumId PlainProps::DeclareNativeEnum ( FEnumDeclarations& Out, EEnumMode Mode )

bool PlainProps::DiffLeaves ( T A, T B )

bool PlainProps::EqualItems ( RangeTypeA&& A, RangeTypeB&& B )

IdType PlainProps::FromIdx ( uint32 Idx )

FMemberId PlainProps::FromIdx ( uint32 Idx )

FInnerId PlainProps::FromIdx ( uint32 Idx )

FParametricTypeId PlainProps::FromIdx ( uint32 Idx )

FEnumId PlainProps::GetEnumId()

TConstArrayView< FRangeBinding > PlainProps::GetRangeBindings()

FBindId PlainProps::GetStructBindId()

FBothStructId PlainProps::GetStructBothId()

FDeclId PlainProps::GetStructDeclId()

FDualStructId PlainProps::GetStructDualId()

std::string_view PlainProps::IllegalArithmetic()

FUnpackedLeafType PlainProps::IllegalLeaf()

ELeafWidth PlainProps::IllegalLeafWidth()

FType PlainProps::IndexArithmeticName()

FType PlainProps::IndexCttiName()

FScopeId PlainProps::IndexNamespaceId ()

FScopeId PlainProps::IndexNamespaceId ()

FType PlainProps::IndexParameterName()

FType PlainProps::IndexParametricType ( FType TemplatedType, const std::tuple< Ts... >* )

FBothStructId PlainProps::IndexStructBothId ( FType DeclName )

FDualStructId PlainProps::IndexStructDualId ( FType Name )

FType PlainProps::IndexStructName()

T PlainProps::LoadSole ( FStructLoadView Src )

void PlainProps::LoadSole ( void* Dst, FStructLoadView Src )

FDeclId PlainProps::LowerCast ( FBindId Id )

FMemberSchema PlainProps::MakeDynamicStructRangeSchema ( ESizeType SizeType )

FMemberSchema PlainProps::MakeEnumRangeSchema ( FEnumId Id )

FMemberSchema PlainProps::MakeEnumRangeSchema ( FEnumId Id, ESizeType MaxSize )

FMemberSchema PlainProps::MakeLeafRangeSchema ()

FMemberSchema PlainProps::MakeLeafRangeSchema ( ESizeType MaxSize )

FUnpackedLeafType PlainProps::MakeLeafType()

FSaveContext PlainProps::MakeSaveContext ( FScratchAllocator& Scratch )

FTypedRange PlainProps::MakeStructRange ( FStructId Id, ESizeType SizeType, FBuiltRange* Values )

FMemberSchema PlainProps::MakeStructRangeSchema ( ESizeType SizeType, FStructId Id )

uint64 PlainProps::Max ( ESizeType Width )

bool PlainProps::operator== ( FMemberSchema A, FMemberSchema B )

TOptional< T > PlainProps::Parse ( FUtf8StringView String )

TOptional< ESizeType > PlainProps::Parse ( FUtf8StringView String )

TOptional< ELeafWidth > PlainProps::Parse ( FUtf8StringView String )

TOptional< FUnpackedLeafType > PlainProps::Parse ( FUtf8StringView String )

TOptional< bool > PlainProps::Parse ( FUtf8StringView String )

TOptional< int8 > PlainProps::Parse ( FUtf8StringView String )

TOptional< int16 > PlainProps::Parse ( FUtf8StringView String )

TOptional< int32 > PlainProps::Parse ( FUtf8StringView String )

TOptional< int64 > PlainProps::Parse ( FUtf8StringView String )

TOptional< uint8 > PlainProps::Parse ( FUtf8StringView String )

TOptional< uint16 > PlainProps::Parse ( FUtf8StringView String )

TOptional< uint32 > PlainProps::Parse ( FUtf8StringView String )

TOptional< uint64 > PlainProps::Parse ( FUtf8StringView String )

TOptional< float > PlainProps::Parse ( FUtf8StringView String )

TOptional< double > PlainProps::Parse ( FUtf8StringView String )

TOptional< char > PlainProps::Parse ( FUtf8StringView String )

TOptional< char8_t > PlainProps::Parse ( FUtf8StringView String )

TOptional< char16_t > PlainProps::Parse ( FUtf8StringView String )

TOptional< char32_t > PlainProps::Parse ( FUtf8StringView String )

void PlainProps::Print ( FUtf8Builder& Out, ESizeType Value )

void PlainProps::Print ( FUtf8Builder& Out, ELeafWidth Value )

void PlainProps::Print ( FUtf8Builder& Out, bool Value )

void PlainProps::Print ( FUtf8Builder& Out, int8 Value )

void PlainProps::Print ( FUtf8Builder& Out, int16 Value )

void PlainProps::Print ( FUtf8Builder& Out, int32 Value )

void PlainProps::Print ( FUtf8Builder& Out, int64 Value )

void PlainProps::Print ( FUtf8Builder& Out, uint8 Value )

void PlainProps::Print ( FUtf8Builder& Out, uint16 Value )

void PlainProps::Print ( FUtf8Builder& Out, uint32 Value )

void PlainProps::Print ( FUtf8Builder& Out, uint64 Value )

void PlainProps::Print ( FUtf8Builder& Out, float Value )

void PlainProps::Print ( FUtf8Builder& Out, double Value )

void PlainProps::Print ( FUtf8Builder& Out, char8_t Value )

void PlainProps::Print ( FUtf8Builder& Out, char16_t Value )

void PlainProps::Print ( FUtf8Builder& Out, char32_t Value )

void PlainProps::Private::Append ( char*& ToIt, std::string_view From )

ESizeType PlainProps::RangeSizeOf ( bool )

ESizeType PlainProps::RangeSizeOf ( int8 )

ESizeType PlainProps::RangeSizeOf ( int16 )

ESizeType PlainProps::RangeSizeOf ( int32 )

ESizeType PlainProps::RangeSizeOf ( int64 )

ESizeType PlainProps::RangeSizeOf ( uint8 )

ESizeType PlainProps::RangeSizeOf ( uint16 )

ESizeType PlainProps::RangeSizeOf ( uint32 )

ESizeType PlainProps::RangeSizeOf ( uint64 )

FMemberType PlainProps::ReflectInnermostType()

std::string_view PlainProps::SelectStructName()

SIZE_T PlainProps::SizeOf ( ELeafWidth Width )

SIZE_T PlainProps::SizeOf ( ESizeType Width )

FMemberSpec PlainProps::Specify ()

FMemberSpec PlainProps::Specify ( FEnumId Id )

FAnsiStringView PlainProps::ToAnsiView ( std::string_view Str )

uint32 PlainProps::ToIdx ( FInnerId Id )

uint32 PlainProps::ToIdx ( FNameId Id )

uint32 PlainProps::ToIdx ( FMemberId Name )

uint32 PlainProps::ToIdx ( FEnumId Id )

uint32 PlainProps::ToIdx ( FStructId Id )

uint32 PlainProps::ToIdx ( FSchemaId Id )

uint32 PlainProps::ToIdx ( FNestedScopeId Id )

uint32 PlainProps::ToIdx ( FParametricTypeId Id )

uint32 PlainProps::ToIdx ( FConcreteTypenameId Name )

TOptionalId< IdType > PlainProps::ToOptional ( IdType Id )

FOptionalDeclId PlainProps::ToOptionalDeclId ( FOptionalInnerId In )

FOptionalEnumId PlainProps::ToOptionalEnum ( FOptionalInnerId In )

FOptionalEnumSchemaId PlainProps::ToOptionalEnum ( FOptionalSchemaId In )

FOptionalInnerId PlainProps::ToOptionalInner ( FOptionalEnumId In )

FOptionalInnerId PlainProps::ToOptionalInner ( FOptionalStructId In )

FOptionalStructId PlainProps::ToOptionalStruct ( FOptionalInnerId In )

FOptionalStructId PlainProps::ToOptionalStruct ( FOptionalDeclId In )

FOptionalStructId PlainProps::ToOptionalStruct ( FOptionalBindId In )

FOptionalStructSchemaId PlainProps::ToOptionalStruct ( FOptionalSchemaId In )

bool PlainProps::Track ( bool bDiff, const FBindContext&, FMemberBindType, FMemberId, FDiffMetadata, const void*, const void* )

bool PlainProps::Track ( bool bDiff, FDiffContext& Ctx, FMemberBindType Type, FMemberId Name, FDiffMetadata Meta, const void* A, const void* B )

FUnpackedLeafType PlainProps::UnpackNonBitfield ( FLeafBindType Packed )

FBindId PlainProps::UpCast ( FDeclId Id )

uint64 PlainProps::ValueCast ( bool Value )

uint64 PlainProps::ValueCast ( int8 Value )

uint64 PlainProps::ValueCast ( int16 Value )

uint64 PlainProps::ValueCast ( int32 Value )

uint64 PlainProps::ValueCast ( int64 Value )

uint64 PlainProps::ValueCast ( uint8 Value )

uint64 PlainProps::ValueCast ( uint16 Value )

uint64 PlainProps::ValueCast ( uint32 Value )

uint64 PlainProps::ValueCast ( uint64 Value )

uint64 PlainProps::ValueCast ( char8_t Value )

uint64 PlainProps::ValueCast ( char16_t Value )

uint64 PlainProps::ValueCast ( char32_t Value )

ELeafWidth PlainProps::WidthOf ( SIZE_T Size )

void PlainProps::WriteAlignedArray ( TArray64< uint8 >& Out, TArrayView< T > In )

void PlainProps::WriteAlignmentPadding ( TArray64< uint8 >& Out )

void PlainProps::WriteArray ( TArray64< uint8 >& Out, const ArrayType& In )

void PlainProps::WriteData ( TArray64< uint8 >& Out, const void* Data, int64 Size )

void PlainProps::WriteInt ( TArray64< uint8 >& Out, T Number )

FVector_Ctti UE::Math::CttiOfPtr ( FVector* )

FVector4_Ctti UE::Math::CttiOfPtr ( FVector4* )

FQuat_Ctti UE::Math::CttiOfPtr ( FQuat* )

static void PlainProps::ForEachVar ( Fn&& Visitor )

static void PlainProps::KeepDebugInfo ( FStructSchemaId* )

static void PlainProps::KeepDebugInfo ( FEnumSchemaId* )

static ELeafBindType PlainProps::ToLeafBindType ( ELeafType Type )

static ELeafType PlainProps::ToLeafType ( ELeafBindType Type )

static FLeafType PlainProps::ToLeafType ( FLeafBindType Leaf )

static FUnpackedLeafType PlainProps::ToUnpackedLeafType ( FUnpackedLeafBindType Leaf )



---

## PlanarCut

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PlanarCut

**Contents:**
- PlanarCut
- Navigation
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

int32 AddCollisionSampleVertices ( double TargetSpacing, FGeometryCollection& Collection, const TArrayView< const int32 >& TransformIndices )

void ConvertGeometryCollectionToDynamicMesh ( UE::Geometry::FDynamicMesh3& OutputMesh, FTransform& TransformOut, bool bCenterPivot, const FGeometryCollection& Collection, bool bWeldEdges, TArrayView< const FTransform3f > BoneTransforms, bool bUseRelativeTransforms, TArrayView< const int32 > TransformIndices, TFunction< int32(int32, bool)> RemapMaterialIDs, bool bAllowInvisible, bool bSetPolygroupPerBone )

UE::Geometry::FDynamicMesh3 ConvertMeshDescriptionToCuttingDynamicMesh ( const FMeshDescription* CuttingMesh, int32 NumUVLayers, FProgressCancel* Progress )

void ConvertToMeshDescription ( FMeshDescription& OutputMesh, FTransform& TransformOut, bool bCenterPivot, FGeometryCollection& Collection, const TManagedArray< FTransform >& BoneTransforms, const TArrayView< const int32 >& TransformIndices, TFunction< int32(int32, bool)> RemapMaterialIDs )

void ConvertToMeshDescription ( FMeshDescription& OutputMesh, FTransform& TransformOut, bool bCenterPivot, FGeometryCollection& Collection, const TManagedArray< FTransform3f >& BoneTransforms, const TArrayView< const int32 >& TransformIndices, TFunction< int32(int32, bool)> RemapMaterialIDs )

void CreateCuttingSurfacePreview ( const FPlanarCells& Cells, const FBox& Bounds, double Grout, int32 RandomSeed, UE::Geometry::FDynamicMesh3& OutCuttingMeshes, TFunctionRef< bool(int)> FilterCellsFunc, const TOptional< FTransform >& TransformCollection, FProgressCancel* Progress, FVector CellsOrigin )

int32 CutMultipleWithMultiplePlanes ( const TArrayView< const FPlane >& Planes, FInternalSurfaceMaterials& InternalSurfaceMaterials, FGeometryCollection& Collection, const TArrayView< const int32 >& TransformIndices, double Grout, double CollisionSampleSpacing, int32 RandomSeed, const TOptional< FTransform >& TransformCollection, bool bSetDefaultInternalMaterialsFromCollection, FProgressCancel* Progress, bool bSplitIslands )

int32 CutMultipleWithPlanarCells ( FPlanarCells& Cells, FGeometryCollection& Collection, const TArrayView< const int32 >& TransformIndices, double Grout, double CollisionSampleSpacing, int32 RandomSeed, const TOptional< FTransform >& TransformCollection, bool bIncludeOutsideCellInOutput, bool bSetDefaultInternalMaterialsFromCollection, FProgressCancel* Progress, FVector CellsOrigin, bool bSplitIslands )

int32 CutWithMesh ( const UE::Geometry::FDynamicMesh3& CuttingMesh, FTransform CuttingMeshTransform, FInternalSurfaceMaterials& InternalSurfaceMaterials, FGeometryCollection& Collection, const TArrayView< const int32 >& TransformIndices, double CollisionSampleSpacing, const TOptional< FTransform >& TransformCollection, bool bSetDefaultInternalMaterialsFromCollection, FProgressCancel* Progress, bool bSplitIslands )

int32 CutWithMesh ( const FMeshDescription* CuttingMesh, FTransform CuttingMeshTransform, FInternalSurfaceMaterials& InternalSurfaceMaterials, FGeometryCollection& Collection, const TArrayView< const int32 >& TransformIndices, double CollisionSampleSpacing, const TOptional< FTransform >& TransformCollection, bool bSetDefaultInternalMaterialsFromCollection, FProgressCancel* Progress, bool bSplitIslands )

int32 CutWithPlanarCells ( FPlanarCells& Cells, FGeometryCollection& Collection, int32 TransformIdx, double Grout, double CollisionSampleSpacing, int32 RandomSeed, const TOptional< FTransform >& TransformCollection, bool bIncludeOutsideCellInOutput, bool bSetDefaultInternalMaterialsFromCollection, FProgressCancel* Progress, FVector CellsOrigin, bool bSplitIslands )

void FilterBonesByVolume ( const FGeometryCollection& Collection, const TArrayView< const int32 >& TransformIndices, const TArrayView< const double >& Volumes, TFunctionRef< bool(double Volume, int32 BoneIdx)> Filter, TArray< int32 >& OutSmallBones, bool bIncludeClusters )

void FindBoneVolumes ( FGeometryCollection& Collection, const TArrayView< const int32 >& TransformIndices, TArray< double >& OutVolumes, double ScalePerDimension, bool bIncludeClusters )

void FindSmallBones ( const FGeometryCollection& Collection, const TArrayView< const int32 >& TransformIndices, const TArrayView< const double >& Volumes, double MinVolume, TArray< int32 >& OutSmallBones, bool bIncludeClusters )

void MergeAllSelectedBones ( FGeometryCollection& Collection, const TArrayView< const int32 >& TransformIndices, bool bUnionJoinedPieces )

int32 MergeBones ( FGeometryCollection& Collection, const TArrayView< const int32 >& TransformIndices, const TArrayView< const double >& Volumes, double MinVolume, const TArrayView< const int32 >& SmallTransformIndices, bool bUnionJoinedPieces, UE::PlanarCut::ENeighborSelectionMethod NeighborSelectionMethod, bool bUseCollectionProximity, bool bOnlySameParent )

void MergeClusters ( FGeometryCollection& Collection, const TArrayView< const double >& Volumes, double MinVolume, const TArrayView< const int32 >& SmallTransformIndices, UE::PlanarCut::ENeighborSelectionMethod NeighborSelectionMethod, bool bOnlyMergeInProximity, bool bOnlySameParent, bool bUseCollectionProximity )

void RecomputeNormalsAndTangents ( bool bOnlyTangents, bool bMakeSharpEdges, float SharpAngleDegrees, FGeometryCollection& Collection, const TArrayView< const int32 >& TransformIndices, bool bOnlyInternalSurfaces )

int32 SplitIslands ( FGeometryCollection& Collection, const TArrayView< const int32 >& TransformIndices, double CollisionSampleSpacing, FProgressCancel* Progress )

bool UE::PlanarCut::BoxProjectUVs ( int32 TargetUVLayer, FGeometryCollection& Collection, const FVector3d& BoxDimensions, EUseMaterials MaterialsPattern, TArrayView< int32 > WhichMaterials, FVector2f OffsetUVs, bool bOverrideBoxDimensionsWithBounds, bool bCenterBoxAtPivot, bool bUniformProjectionScale )

bool UE::PlanarCut::UVLayout ( int32 TargetUVLayer, FGeometryCollection& Collection, int32 UVRes, float GutterSize, EUseMaterials MaterialsPattern, TArrayView< int32 > WhichMaterials, bool bRecreateUVsForDegenerateIslands, FProgressCancel* Progress )



---

## PlatformCryptoContext

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PlatformCryptoContext

**Contents:**
- PlatformCryptoContext
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## PlatformCryptoTypes

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PlatformCryptoTypes

**Contents:**
- PlatformCryptoTypes
- Navigation
- Classes
- Interfaces
- Enums
  - Public
- Variables
  - Public



---

## PlatformCrypto

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PlatformCrypto

**Contents:**
- PlatformCrypto
- Navigation
- Interfaces



---

## PlayTimeLimit

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PlayTimeLimit

**Contents:**
- PlayTimeLimit
- Navigation
- Classes
- Structs
- Typedefs



---

## PluginBrowser

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PluginBrowser

**Contents:**
- PluginBrowser
- Navigation
- Interfaces
- Typedefs



---

## PluginReferenceViewer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PluginReferenceViewer

**Contents:**
- PluginReferenceViewer
- Navigation
- Classes



---

## Plugins

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/plugins-in-unreal-engine

**Contents:**
- Plugins
- Plugin UI in the Editor
- Anatomy of a Plugin
- Plugin Folders
- Code in Plugins
  - Engine Plugins
- Content in Plugins
- Plugins in Projects
- Distributing a Plugin on the Epic Marketplace
  - Precompiling Plugins

How to create Unreal Engine plugins.

This page describes the development and management of Plugins for use with Unreal Engine (UE) tools and runtime.

In Unreal Engine, Plugins are collections of code and data that developers can easily enable or disable within the Editor on a per-project basis. Plugins can add runtime gameplay functionality, modify built-in Engine features (or add new ones), create new file types, and extend the capabilities of the Editor with new menus, tool bar commands, and sub-modes. Many existing Unreal Engine subsystems were designed to be extensible using Plugins.

If you want to jump right in and create a Plugin now, please see the Creating New Plugins section.

You can see which Plugins are currently installed by opening the Plugin editing interface from the Edit menu.

The Plugin Editor is accessible from the main 'Window' menu. This interface displays all of the Plugins that are currently installed and can enable or disable Plugins individually.

You can browse categories of Plugins using the tree interface on the left. Selecting a category will show all Plugins in that category as well as Plugins in any sub-category. As you navigate through categories, a bread crumb trail displayed at the top of the UI will enable you to jump quickly to higher-level categories. The number displayed next to a category indicates how many Plugins are available in that category.

Plugins are displayed in the main list, along with each Plugin's name, icon, current version, text description, author (and optional web hyperlink), as well as whether or not the plugin is currently enabled.

The search control at the top will enable you to search Plugins displayed in the list by name.

You can enable or disable a Plugin for use with your active project by toggling the Enabled check box under the Plugin's description. You may need to restart the Editor for the change to take effect.

Plugins with code will have a Source folder. This folder will contain one or more directories with module source code for the Plugin. Note that, although Plugins often contain code, this is not actually a requirement. See the Code in Plugins section for more information.

Plugins with code will have a Binaries folder that contains compiled code for that Plugin, and temporary build product files will be stored in a separate Intermediate folder under the Plugin's directory.

Plugins can have their own Content folder that contains Asset files specific to that Plugin. See the Content in Plugins section for more information. Plugin configuration files should be placed using the same convention as other configuration files:

Plugins do not support their own Derived Data Cache distribution.

In order for Plugins to be found, they must be located in one of the search paths for Plugins, either in your project, or in the Engine itself.

You can also organize Plugins into subdirectories under the base Plugins folder. The engine will scan all of your sub-folders under the base Plugins folder for Plugins to load, but it will never scan subdirectories beneath a Plugin that has already been found.

Unreal Engine finds your Plugin by searching for .uplugin files on disk. We call these files Plugin Descriptors. They are text files that provide basic information about your Plugin. Plugin Descriptors are discovered and loaded automatically by the Engine, Editor, and UnrealBuildTool (UBT), whenever those programs are run. See the section on Plugin Descriptors to learn about creating and customizing these files.

When generating project files for Visual Studio or Xcode, any Plugins that have Source folders (containing .Build.cs files) will be added to your project files to make it easier to navigate to their source code. These Plugins will automatically be compiled by UBT when compiling your game project.

Plugins are allowed to have any number of Module source directories. Most Plugins will only have one Module, but it is possible to create multiple, for example, if a Plugin contains some Editor-only functionality, and other code that is intended to run during the game.

For the most part, Plugin source file layout is the same as any other C++ Module in the Engine.

Plugins are able to declare new reflected types (UCLASS, USTRUCT, etc.) in header files within a Module's Source directory (or one of its subdirectories). The Engine's build system will detect these files and generate code as needed to support the new types. You will need to follow the normal rules for using UObjects within C++ modules, such as including the generated header file and the Module's generated.inl file in one of your Module's source files.

Unreal Engine supports interdependent Modules and Plugins. Project Modules can depend on Plugins by enabling the Plugins in its .uproject file. Similarly, Plugins indicate dependency by enabling other Plugins within their own .uplugin files. There is one important restriction, however, which is that Plugins and Modules are broken into hierarchical levels, and can only depend on other Plugins or Modules at the same level or higher. For example, although a Project Module can depend on an Engine Module, an Engine Module cannot depend on a Project Module. This is because the Engine (and all of its Plugins and Modules) is higher-level than any Project, as it must be able to build without a Project. The following diagram indicates the hierarchy of dependency levels between Projects and Modules:

Arrows indicate possible dependency. Each Plugin or Module type can depend on others at its own level or higher.

Unreal Engine has some built-in Plugins included under the Engine directory. Engine Plugins are just like project Plugins, except that they are available for all projects. Typically, these plugins are created by engine and tools programmers to provide baseline functionality that can be used in multiple projects while being maintained in a single place. This can enable the user to add or override engine features without modifying engine code.

Unreal Engine supports plugins that contain game content as well as binary code. In order to use Content in a Plugin, the "CanContainContent" setting within the Plugin's descriptor must be set to "true".

Plugins reside under the Plugins subfolder within your project's directory, and will be detected and loaded at Engine or Editor start-up time.

If the Plugin contains modules that have Source folders (and .Build.cs files), Plugin code will automatically be added to generated C++ project files, so that you can work on developing the Plugin alongside your project. Whenever you compile your project, any Plugins that have source available will also be compiled as a dependency of your game.

Plugins that do not have a Source folder are ignored by the project generator and will not appear in your C++ project files, but they will still be loaded at start-up as long as binary files exist.

At present, Plugin configuration files are not packaged with projects. This may be supported in the future, but currently requires manually copying the files to the project's Config folder.

To package your Plugin, click the Package... link to package your Plugin into a folder for distribution.

If you are precompiling a plugin for UE 5.2, compile your plugin with Visual Studio 2019 — the minimum supported version of Visual Studio for UE 5.2. Compiling with Visual Studio 2019 ensures that the resulting libraries are compatible with UE 5.2 for all users. For more information about Visual Studio and Unreal Engine version compatability, see Setting Up Visual Studio for more information.

Plugin descriptors are files that end with .uplugin. The first part of the file name is always the name of your Plugin. Plugin descriptor files are always located in your Plugin's directory, where the Engine will discover them at start-up time.

Plugin descriptors are in the Json (JavaScript Object Notation) file format.

This example plugin descriptor is from the Engine's UObjectPlugin.

The descriptor file is a JSON-formatted list of variables from the FPluginDescriptor type. There is one additional field, "FileVersion", which is the only required field in the structure. "FileVersion" gives the version of the Plugin descriptor file, and should usually set to the highest version that is allowed by the Engine (currently, this is "3"). Because this version applies to the format of the Plugin Descriptor File, and not the Plugin itself, we do not expect that it will change very frequently, and it should not change with subsequent releases of your Plugin. For maximum compatibility with older versions of the Engine, you can use an older version number, but this is not recommended.

For details about the other supported fields, see the API reference page.

For Plugins that contain code, the "Modules" field in the descriptor file will contain at least one entry. An example entry follows:

Each entry requires the "Name" and "Type" fields. "Name" is the unique name of the Plugin Module that will be loaded with the Plugin. At runtime, the Engine will expect appropriate Plugin binaries to exist in the Plugin's "Binaries" folder with the specified Module name. For Modules that have a Source directory, a matching ".Build.cs" file much exist within the Module's subfolder tree. "Type" sets the type of Module. Valid options are Runtime, RuntimeNoCommandlet, Developer, Editor, EditorNoCommandlet, and Program. This type determines which types of applications can load the Module. For example, some plugins may include modules that should only load when the Editor is running. Runtime modules will be loaded in all cases, even in shipped games. Developer modules will only be loaded in development runtime or Editor builds, but never in shipping builds. Editor modules will only be loaded when the editor is starting up. Your Plugin can use a combination of modules of different types.

For details about the other supported fields, see the API reference page.

Along with the descriptor file, Plugins need an icon to display in the Editor's Plugin Browser. The image should be a 128x128 .png file called "Icon128.png" and kept in the Plugin's "/Resources/" directory.

To create a new Plugin, use the New Plugin button in the Editor's Plugin Browser.

From there, you can select which type of Plugin you wish to create, enter a name, and set some basic parameters.

Your new Plugin will now appear in the Plugin Browser, and will be enabled in your current project.



**Examples:**

Example 1 (json):
```json
{
    "FileVersion" : 3,
    "Version" : 1,
    "VersionName" : "1.0",
    "FriendlyName" : "UObject Example Plugin",
    "Description" : "An example of a plugin which declares its own UObject type.  This can be used as a starting point when creating your own plugin.",
    "Category" : "Examples",
    "CreatedBy" : "Epic Games, Inc.",
    "CreatedByURL" : "http://epicgames.com",
    "DocsURL" : "",
    "MarketplaceURL" : "",
    "SupportURL" : "",
    "EnabledByDefault" : true,
    "CanContainContent" : false,
    "IsBetaVersion" : false,
    "Installed" : false,
    "Modules" :
    [
        {
            "Name" : "UObjectPlugin",
            "Type" : "Developer",
            "LoadingPhase" : "Default"
        }
    ]
}
```

Example 2 (json):
```json
{
    "Name" : "UObjectPlugin",
    "Type" : "Developer"
    "LoadingPhase" : "Default"
}
```

---

## Plugins

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins

**Contents:**
- Plugins
- A
- B
- C
- D
- E
- F
- G
- H
- I

Additional optional Developer, Editor, and Runtime functionality.

The Plugins category contains built-in plugin modules that are available for all Unreal Engine projects. These modules are not immediately compiled and may be any of the Developer, Editor, or Runtime types.



---

## Plugins for UI Development

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/plugins-for-ui-development-in-unreal-engine

**Contents:**
- Plugins for UI Development

Learn about plugins that expand your toolset for building user interfaces.



---

## PluginUtils

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PluginUtils

**Contents:**
- PluginUtils
- Navigation
- Classes



---

## PortableObjectFileDataSource

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PortableObjectFileDataSource

**Contents:**
- PortableObjectFileDataSource
- Navigation
- Interfaces



---

## PoseSearchEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PoseSearchEditor

**Contents:**
- PoseSearchEditor
- Navigation
- Classes
- Structs
- Interfaces



---

## PoseSearch

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PoseSearch

**Contents:**
- PoseSearch
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

~FPoseSearchQueryTrajectory()

~FPoseSearchQueryTrajectorySample()

FVector BlendParameterForSampleRanges ( int32 HorizontalBlendIndex, int32 VerticalBlendIndex ) const

void DebugDrawTrajectory ( const UWorld* World, const float DebugThickness, float HeightOffset ) const

void DebugDrawTrajectory ( FAnimInstanceProxy& AnimInstanceProxy, const float DebugThickness, float HeightOffset, int MaxHistorySamples, int MaxPredictionSamples ) const

void DebugDrawTrajectory ( const UObject* Owner, const FLogCategoryBase& Category, ELogVerbosity::Type Verbosity, const float DebugThickness, float HeightOffset ) const

bool EnumHasAnyFlags ( int32 Flags, EPoseSearchBoneFlags Contains )

bool EnumHasAnyFlags ( int32 Flags, EPoseSearchTrajectoryFlags Contains )

FPoseSearchQueryTrajectory ( const FPoseSearchQueryTrajectory& )

FPoseSearchQueryTrajectory ( FPoseSearchQueryTrajectory&& )

FPoseSearchQueryTrajectory ( const FTransformTrajectory& InTrajectory )

FPoseSearchQueryTrajectorySample ( const FPoseSearchQueryTrajectorySample& )

FPoseSearchQueryTrajectorySample ( FPoseSearchQueryTrajectorySample&& )

virtual UObject * GetAnimationAsset()

virtual UAnimationAsset * GetAnimationAssetForRole ( const UE::PoseSearch::FRole& Role ) const

virtual UClass * GetAnimationAssetStaticClass()

void GetBlendSpaceParameterSampleRanges ( int32& HorizontalBlendNum, int32& VerticalBlendNum ) const

virtual FFloatInterval GetEffectiveSamplingRange ( const FVector& BlendParameters ) const

virtual int32 GetNumRoles()

virtual float GetPlayLength ( const FVector& BlendParameters ) const

USkeletalMesh * GetPreviewMeshForRole ( const UE::PoseSearch::FRole& Role ) const

virtual UE::PoseSearch::FRole GetRole ( int32 RoleIndex ) const

virtual FTransform GetRootTransformOriginForRole ( const UE::PoseSearch::FRole& Role ) const

FPoseSearchQueryTrajectorySample GetSampleAtTime ( float Time, bool bExtrapolate ) const

virtual FFloatInterval GetSamplingRange()

FTransform GetTransform()

uint32 GetTypeHash ( const FPoseHistoryAnimationAttribute& Key )

virtual bool IsLooping()

virtual bool IsRootMotionEnabled()

virtual void IterateOverSamplingParameter ( const TFunction< void(const FVector&BlendParameters)>& ProcessSamplingParameter ) const

PRAGMA_DISABLE_DEPRECATION_WARNINGSFPoseSearchQueryTrajectorySample Lerp ( const FPoseSearchQueryTrajectorySample& Other, float Alpha ) const

operator FTransformTrajectory()

bool operator! ( EPoseSearchBoneFlags E )

bool operator! ( EPoseSearchTrajectoryFlags E )

EPoseSearchBoneFlags operator& ( EPoseSearchBoneFlags Lhs, EPoseSearchBoneFlags Rhs )

EPoseSearchTrajectoryFlags operator& ( EPoseSearchTrajectoryFlags Lhs, EPoseSearchTrajectoryFlags Rhs )

EPoseSearchBoneFlags & operator&= ( EPoseSearchBoneFlags& Lhs, EPoseSearchBoneFlags Rhs )

EPoseSearchTrajectoryFlags & operator&= ( EPoseSearchTrajectoryFlags& Lhs, EPoseSearchTrajectoryFlags Rhs )

EPoseSearchBoneFlags operator^ ( EPoseSearchBoneFlags Lhs, EPoseSearchBoneFlags Rhs )

EPoseSearchTrajectoryFlags operator^ ( EPoseSearchTrajectoryFlags Lhs, EPoseSearchTrajectoryFlags Rhs )

EPoseSearchBoneFlags & operator^= ( EPoseSearchBoneFlags& Lhs, EPoseSearchBoneFlags Rhs )

EPoseSearchTrajectoryFlags & operator^= ( EPoseSearchTrajectoryFlags& Lhs, EPoseSearchTrajectoryFlags Rhs )

EPoseSearchBoneFlags operator| ( EPoseSearchBoneFlags Lhs, EPoseSearchBoneFlags Rhs )

EPoseSearchTrajectoryFlags operator| ( EPoseSearchTrajectoryFlags Lhs, EPoseSearchTrajectoryFlags Rhs )

EPoseSearchBoneFlags & operator|= ( EPoseSearchBoneFlags& Lhs, EPoseSearchBoneFlags Rhs )

int32 & operator|= ( int32& Lhs, EPoseSearchBoneFlags Rhs )

EPoseSearchTrajectoryFlags & operator|= ( EPoseSearchTrajectoryFlags& Lhs, EPoseSearchTrajectoryFlags Rhs )

int32 & operator|= ( int32& Lhs, EPoseSearchTrajectoryFlags Rhs )

EPoseSearchBoneFlags operator~ ( EPoseSearchBoneFlags E )

EPoseSearchTrajectoryFlags operator~ ( EPoseSearchTrajectoryFlags E )

FPoseSearchQueryTrajectorySample & operator= ( const FPoseSearchQueryTrajectorySample& )

FPoseSearchQueryTrajectorySample & operator= ( FPoseSearchQueryTrajectorySample&& )

FPoseSearchQueryTrajectory & operator= ( const FPoseSearchQueryTrajectory& )

FPoseSearchQueryTrajectory & operator= ( FPoseSearchQueryTrajectory&& )

bool operator== ( const FPoseSearchDatabaseSequence& A, const FPoseSearchDatabaseSequence& B )

bool operator== ( const FPoseSearchDatabaseBlendSpace& A, const FPoseSearchDatabaseBlendSpace& B )

bool operator== ( const FPoseSearchDatabaseAnimComposite& A, const FPoseSearchDatabaseAnimComposite& B )

bool operator== ( const FPoseSearchDatabaseAnimMontage& A, const FPoseSearchDatabaseAnimMontage& B )

bool operator== ( const FPoseSearchDatabaseMultiAnimAsset& A, const FPoseSearchDatabaseMultiAnimAsset& B )

virtual void SetSamplingRange ( const FFloatInterval& NewRange )

void SetTransform ( const FTransform& Transform )

bool UE::PoseSearch::operator! ( EDebugDrawFlags E )

bool UE::PoseSearch::operator! ( EPoseCandidateFlags E )

bool UE::PoseSearch::operator! ( ERequestAsyncBuildFlag E )

EDebugDrawFlags UE::PoseSearch::operator& ( EDebugDrawFlags Lhs, EDebugDrawFlags Rhs )

EPoseCandidateFlags UE::PoseSearch::operator& ( EPoseCandidateFlags Lhs, EPoseCandidateFlags Rhs )

ERequestAsyncBuildFlag UE::PoseSearch::operator& ( ERequestAsyncBuildFlag Lhs, ERequestAsyncBuildFlag Rhs )

EDebugDrawFlags & UE::PoseSearch::operator&= ( EDebugDrawFlags& Lhs, EDebugDrawFlags Rhs )

EPoseCandidateFlags & UE::PoseSearch::operator&= ( EPoseCandidateFlags& Lhs, EPoseCandidateFlags Rhs )

ERequestAsyncBuildFlag & UE::PoseSearch::operator&= ( ERequestAsyncBuildFlag& Lhs, ERequestAsyncBuildFlag Rhs )

EDebugDrawFlags UE::PoseSearch::operator^ ( EDebugDrawFlags Lhs, EDebugDrawFlags Rhs )

EPoseCandidateFlags UE::PoseSearch::operator^ ( EPoseCandidateFlags Lhs, EPoseCandidateFlags Rhs )

ERequestAsyncBuildFlag UE::PoseSearch::operator^ ( ERequestAsyncBuildFlag Lhs, ERequestAsyncBuildFlag Rhs )

EDebugDrawFlags & UE::PoseSearch::operator^= ( EDebugDrawFlags& Lhs, EDebugDrawFlags Rhs )

EPoseCandidateFlags & UE::PoseSearch::operator^= ( EPoseCandidateFlags& Lhs, EPoseCandidateFlags Rhs )

ERequestAsyncBuildFlag & UE::PoseSearch::operator^= ( ERequestAsyncBuildFlag& Lhs, ERequestAsyncBuildFlag Rhs )

EDebugDrawFlags UE::PoseSearch::operator| ( EDebugDrawFlags Lhs, EDebugDrawFlags Rhs )

EPoseCandidateFlags UE::PoseSearch::operator| ( EPoseCandidateFlags Lhs, EPoseCandidateFlags Rhs )

ERequestAsyncBuildFlag UE::PoseSearch::operator| ( ERequestAsyncBuildFlag Lhs, ERequestAsyncBuildFlag Rhs )

PRAGMA_DISABLE_DEPRECATION_WARNINGS constexpr EDebugDrawFlags & UE::PoseSearch::operator|= ( EDebugDrawFlags& Lhs, EDebugDrawFlags Rhs )

EPoseCandidateFlags & UE::PoseSearch::operator|= ( EPoseCandidateFlags& Lhs, EPoseCandidateFlags Rhs )

ERequestAsyncBuildFlag & UE::PoseSearch::operator|= ( ERequestAsyncBuildFlag& Lhs, ERequestAsyncBuildFlag Rhs )

EDebugDrawFlags UE::PoseSearch::operator~ ( EDebugDrawFlags E )

EPoseCandidateFlags UE::PoseSearch::operator~ ( EPoseCandidateFlags E )

ERequestAsyncBuildFlag UE::PoseSearch::operator~ ( ERequestAsyncBuildFlag E )

int32 UE::PoseSearch::TAlignOf()

int32 UE::PoseSearch::TMax ( int32 A, int32 B )

UE_TRACE_CHANNEL_EXTERN ( PoseSearchChannel )

static void UE::PoseSearch::GenerateCombinations ( int32 DataCardinality, int32 CombinationCardinality, EvaluateCombinationType EvaluateCombination )

static void UE::PoseSearch::GenerateCombinationsRecursive ( int32 DataCardinality, int32 DataIndex, TArrayView< int32 > Combination, int32 CombinationIndex, EvaluateCombinationType EvaluateCombination )

static bool UE::PoseSearch::IsValid ( const FRoleToIndex& RoleToIndex )

static FRoleToIndex UE::PoseSearch::MakeRoleToIndex ( const TConstArrayView< FRole > Roles )



---

## PPMChainGraphEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PPMChainGraphEditor

**Contents:**
- PPMChainGraphEditor
- Navigation
- Interfaces



---

## PPMChainGraph

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PPMChainGraph

**Contents:**
- PPMChainGraph
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## PreLoadScreenMoviePlayer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PreLoadScreenMoviePlayer

**Contents:**
- PreLoadScreenMoviePlayer
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

DEFINE_LOG_CATEGORY_STATIC ( LogPreloadMoviePlayer, Log, All )



---

## ProceduralMeshComponentEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ProceduralMeshComponentEditor

**Contents:**
- ProceduralMeshComponentEditor
- Navigation
- Interfaces



---

## ProceduralMeshComponent

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ProceduralMeshComponent

**Contents:**
- ProceduralMeshComponent
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

FMeshDescriptionPROCEDURALMESHCOMPONENT_API BuildMeshDescription ( UProceduralMeshComponent* ProcMeshComp )

void PROCEDURALMESHCOMPONENT_API MeshDescriptionToProcMesh ( const FMeshDescription& MeshDescription, UProceduralMeshComponent* ProcMeshComp )



---

## ProceduralVegetationEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ProceduralVegetationEditor

**Contents:**
- ProceduralVegetationEditor
- Navigation
- Classes
- Enums
  - Public
- Variables
  - Public



---

## ProceduralVegetation

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ProceduralVegetation

**Contents:**
- ProceduralVegetation
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Functions

bool operator! ( EPVRenderType E )

EPVRenderType operator& ( EPVRenderType Lhs, EPVRenderType Rhs )

EPVRenderType & operator&= ( EPVRenderType& Lhs, EPVRenderType Rhs )

EPVRenderType operator^ ( EPVRenderType Lhs, EPVRenderType Rhs )

EPVRenderType & operator^= ( EPVRenderType& Lhs, EPVRenderType Rhs )

EPVRenderType operator| ( EPVRenderType Lhs, EPVRenderType Rhs )

EPVRenderType & operator|= ( EPVRenderType& Lhs, EPVRenderType Rhs )

EPVRenderType operator~ ( EPVRenderType E )

static void PV::FillAttributes ( FManagedArrayCollection& Collection, const FName Group, const TSharedPtr< FJsonObject >& AttributesObject )

static void PV::FillDetailsAttributes ( FManagedArrayCollection& Collection, const FName Group, const TSharedPtr< FJsonObject >& AttributesObject )

static void PV::FillFoliageData ( FManagedArrayCollection& Collection, const TSharedPtr< FJsonObject >& PrimitiveAttributesObject, const FString& InPath )

static void PV::FillPlantProfilesData ( FManagedArrayCollection& Collection, const FName Group, const TSharedPtr< FJsonObject >& AttributesObject )

static bool PV::HasJsonFieldPath ( const TSharedPtr< FJsonObject >& JsonObject, const FString& Path )

static bool PV::LoadMegaPlantsJsonToCollection ( FManagedArrayCollection& Collection, const FString& FilePath, FString& OutErrorMessage )

static TSharedPtr< FJsonObject > PV::LoadMetaFileIntoJsonObject ( const FString& FilePath, FString& OutErrorMessage )

static bool PV::LoadMetaJsonToCollection ( FManagedArrayCollection& Collection, TSharedPtr< FJsonObject > LoadedData )

static void PV::SetFoliagePaths ( FManagedArrayCollection& Collection, const FString& FilePath )



---

## ProjectLauncher

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ProjectLauncher

**Contents:**
- ProjectLauncher
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## Project Settings

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/project-settings-in-unreal-engine

**Contents:**
- Project Settings
- Accessing Project Settings
- Categories and Sections

An overview of the project settings in Unreal Engine.

The Project Settings window provides access to configuration options that affect:

Some plugins also append their configuration options to the Project Settings window.

All of the settings in this window are stored in your project's default engine configuration file (Engine.ini). The Project Settings window provides a visual, intuitive, and searchable user interface for editing these. You can also manually edit the Engine.ini file to change individual settings.

To open the Project Settings window, from Unreal Engine's main menu, go to Edit > Project Settings.

The Project Settings window is divided up into categories and sections of related options. Select a category from the navigation on the left to open its associated settings in the right-hand panel. You can also search for a specific option by name.

You can export the settings into a backup file on your computer or import settings from the file by clicking Export or Import in the upper-right corner of the Project Settings window.

The editor .ini file is updated every time you change something in the Project Settings, and the values in it apply to all platforms. The editor .ini file is in <ProjectDirectory>\Config\DefaultEngine.ini.

Platform .ini files have to be edited manually in a text editor and only apply to a specific platform. An example of a platform .ini file is <ProjectDirectory>\Config\Windows\WindowsEngine.ini

The Project Settings window contains the following sections and categories:



---

## PropertyAnimatorCoreEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PropertyAnimatorCoreEditor

**Contents:**
- PropertyAnimatorCoreEditor
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## PropertyAnimatorCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PropertyAnimatorCore

**Contents:**
- PropertyAnimatorCore
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## PropertyAnimator

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PropertyAnimator

**Contents:**
- PropertyAnimator
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

bool EvaluateChannel ( const UMovieSceneSection* InSection, const FPropertyAnimatorEasingDoubleChannel* InChannel, FFrameTime InTime, double& OutValue )

bool EvaluateChannel ( const UMovieSceneSection* InSection, const FPropertyAnimatorWaveDoubleChannel* InChannel, FFrameTime InTime, double& OutValue )

float UE::PropertyAnimator::Easing::Back ( float InProgress, EPropertyAnimatorEasingType InType )

float UE::PropertyAnimator::Easing::Bounce ( float InProgress, EPropertyAnimatorEasingType InType )

float UE::PropertyAnimator::Easing::Circ ( float InProgress, EPropertyAnimatorEasingType InType )

float UE::PropertyAnimator::Easing::Cubic ( float InProgress, EPropertyAnimatorEasingType InType )

float UE::PropertyAnimator::Easing::Ease ( float InProgress, EPropertyAnimatorEasingFunction InFunction, EPropertyAnimatorEasingType InType )

float UE::PropertyAnimator::Easing::Elastic ( float InProgress, EPropertyAnimatorEasingType InType )

float UE::PropertyAnimator::Easing::Expo ( float InProgress, EPropertyAnimatorEasingType InType )

float UE::PropertyAnimator::Easing::Linear ( float InProgress, EPropertyAnimatorEasingType InType )

float UE::PropertyAnimator::Easing::Quad ( float InProgress, EPropertyAnimatorEasingType InType )

float UE::PropertyAnimator::Easing::Quart ( float InProgress, EPropertyAnimatorEasingType InType )

float UE::PropertyAnimator::Easing::Quint ( float InProgress, EPropertyAnimatorEasingType InType )

float UE::PropertyAnimator::Easing::Sine ( float InProgress, EPropertyAnimatorEasingType InType )

double UE::PropertyAnimator::Wave::Bounce ( double InTime, double InAmplitude, double InFrequency, double InOffset )

double UE::PropertyAnimator::Wave::Cosine ( double InTime, double InAmplitude, double InFrequency, double InOffset )

double UE::PropertyAnimator::Wave::InvertedSquare ( double InTime, double InAmplitude, double InFrequency, double InOffset )

double UE::PropertyAnimator::Wave::Perlin ( double InTime, double InAmplitude, double InFrequency, double InOffset )

double UE::PropertyAnimator::Wave::Pulse ( double InTime, double InAmplitude, double InFrequency, double InOffset )

double UE::PropertyAnimator::Wave::Sawtooth ( double InTime, double InAmplitude, double InFrequency, double InOffset )

double UE::PropertyAnimator::Wave::Sine ( double InTime, double InAmplitude, double InFrequency, double InOffset )

double UE::PropertyAnimator::Wave::Square ( double InTime, double InAmplitude, double InFrequency, double InOffset )

double UE::PropertyAnimator::Wave::Triangle ( double InTime, double InAmplitude, double InFrequency, double InOffset )

double UE::PropertyAnimator::Wave::Wave ( double InTime, double InAmplitude, double InFrequency, double InOffset, EPropertyAnimatorWaveFunction InFunction )



---

## PropertyBindingUtilsEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PropertyBindingUtilsEditor

**Contents:**
- PropertyBindingUtilsEditor
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## PropertyBindingUtilsTestSuite

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PropertyBindingUtilsTestSuite

**Contents:**
- PropertyBindingUtilsTestSuite
- Navigation
- Interfaces



---

## PropertyBindingUtils

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PropertyBindingUtils

**Contents:**
- PropertyBindingUtils
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

void UE::PropertyBinding::CreateUniquelyNamedPropertiesInPropertyBag ( TArrayView< FPropertyCreationDescriptor > InOutCreationDescs, FInstancedPropertyBag& OutPropertyBag )

FString UE::PropertyBinding::GetDescriptorAndPathAsString ( const FPropertyBindingBindableStructDescriptor& InDescriptor, const FPropertyBindingPath& InPath )

EPropertyCompatibility UE::PropertyBinding::GetPropertyCompatibility ( const FProperty* FromProperty, const FProperty* ToProperty )



---

## ProxyLODMeshReduction

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ProxyLODMeshReduction

**Contents:**
- ProxyLODMeshReduction
- Navigation
- Interfaces



---

## ProxyTable

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ProxyTable

**Contents:**
- ProxyTable
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Functions
  - Public

uint32 GetTypeHash ( const FProxyEntry& Entry )



---

## PSDImporterCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PSDImporterCore

**Contents:**
- PSDImporterCore
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

bool UE::PSDImporter::File::operator! ( EPSDLayerFlags E )

EPSDLayerFlags UE::PSDImporter::File::operator& ( EPSDLayerFlags Lhs, EPSDLayerFlags Rhs )

EPSDLayerFlags & UE::PSDImporter::File::operator&= ( EPSDLayerFlags& Lhs, EPSDLayerFlags Rhs )

EPSDLayerFlags UE::PSDImporter::File::operator^ ( EPSDLayerFlags Lhs, EPSDLayerFlags Rhs )

EPSDLayerFlags & UE::PSDImporter::File::operator^= ( EPSDLayerFlags& Lhs, EPSDLayerFlags Rhs )

EPSDLayerFlags UE::PSDImporter::File::operator| ( EPSDLayerFlags Lhs, EPSDLayerFlags Rhs )

EPSDLayerFlags & UE::PSDImporter::File::operator|= ( EPSDLayerFlags& Lhs, EPSDLayerFlags Rhs )

EPSDLayerFlags UE::PSDImporter::File::operator~ ( EPSDLayerFlags E )



---

## PSDImporter

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PSDImporter

**Contents:**
- PSDImporter
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Functions
  - Public

uint32 GetTypeHash ( const FPSDFileLayerId& InValue )

uint32 GetTypeHash ( const FPSDFileLayer& InValue )

bool operator! ( EPSDFileLayerImportOperation E )

bool operator! ( EPSDImporterLayerMaterialType E )

EPSDFileLayerImportOperation operator& ( EPSDFileLayerImportOperation Lhs, EPSDFileLayerImportOperation Rhs )

EPSDImporterLayerMaterialType operator& ( EPSDImporterLayerMaterialType Lhs, EPSDImporterLayerMaterialType Rhs )

EPSDFileLayerImportOperation & operator&= ( EPSDFileLayerImportOperation& Lhs, EPSDFileLayerImportOperation Rhs )

EPSDImporterLayerMaterialType & operator&= ( EPSDImporterLayerMaterialType& Lhs, EPSDImporterLayerMaterialType Rhs )

EPSDFileLayerImportOperation operator^ ( EPSDFileLayerImportOperation Lhs, EPSDFileLayerImportOperation Rhs )

EPSDImporterLayerMaterialType operator^ ( EPSDImporterLayerMaterialType Lhs, EPSDImporterLayerMaterialType Rhs )

EPSDFileLayerImportOperation & operator^= ( EPSDFileLayerImportOperation& Lhs, EPSDFileLayerImportOperation Rhs )

EPSDImporterLayerMaterialType & operator^= ( EPSDImporterLayerMaterialType& Lhs, EPSDImporterLayerMaterialType Rhs )

EPSDFileLayerImportOperation operator| ( EPSDFileLayerImportOperation Lhs, EPSDFileLayerImportOperation Rhs )

EPSDImporterLayerMaterialType operator| ( EPSDImporterLayerMaterialType Lhs, EPSDImporterLayerMaterialType Rhs )

EPSDFileLayerImportOperation & operator|= ( EPSDFileLayerImportOperation& Lhs, EPSDFileLayerImportOperation Rhs )

EPSDImporterLayerMaterialType & operator|= ( EPSDImporterLayerMaterialType& Lhs, EPSDImporterLayerMaterialType Rhs )

EPSDFileLayerImportOperation operator~ ( EPSDFileLayerImportOperation E )

EPSDImporterLayerMaterialType operator~ ( EPSDImporterLayerMaterialType E )



---

## PythonAutomationTest

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PythonAutomationTest

**Contents:**
- PythonAutomationTest
- Navigation
- Classes



---

## PythonScriptPlugin

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/PythonScriptPlugin

**Contents:**
- PythonScriptPlugin
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

void LexFromString ( EPythonCommandExecutionMode& OutMode, const TCHAR* InBuffer )

const TCHAR * LexToString ( EPythonLogOutputType InType )

const TCHAR * LexToString ( EPythonCommandExecutionMode InMode )

bool LexTryParseString ( EPythonCommandExecutionMode& OutMode, const TCHAR* InBuffer )

bool operator! ( EPythonCommandFlags E )

EPythonCommandFlags operator& ( EPythonCommandFlags Lhs, EPythonCommandFlags Rhs )

EPythonCommandFlags & operator&= ( EPythonCommandFlags& Lhs, EPythonCommandFlags Rhs )

EPythonCommandFlags operator^ ( EPythonCommandFlags Lhs, EPythonCommandFlags Rhs )

EPythonCommandFlags & operator^= ( EPythonCommandFlags& Lhs, EPythonCommandFlags Rhs )

EPythonCommandFlags operator| ( EPythonCommandFlags Lhs, EPythonCommandFlags Rhs )

EPythonCommandFlags & operator|= ( EPythonCommandFlags& Lhs, EPythonCommandFlags Rhs )

EPythonCommandFlags operator~ ( EPythonCommandFlags E )



---

## Qos

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Qos

**Contents:**
- Qos
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Functions
  - Public

const TCHAR * LexToString ( EQosDatacenterResult Result )

const TCHAR * LexToString ( EQosCompletionResult Result )



---

## QuicMessagingTransport

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/QuicMessagingTransport

**Contents:**
- QuicMessagingTransport
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## QuicMessaging

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/QuicMessaging

**Contents:**
- QuicMessaging
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## RawInput

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RawInput

**Contents:**
- RawInput
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## RazerChromaDevices

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RazerChromaDevices

**Contents:**
- RazerChromaDevices
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

ENUM_CLASS_FLAGS ( ERazerChromaDeviceTypes )



---

## Reflex

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Reflex

**Contents:**
- Reflex
- Navigation
- Classes
- Enums
  - Public



---

## Rejoin

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Rejoin

**Contents:**
- Rejoin
- Navigation
- Classes
- Typedefs
- Enums
  - Public
- Functions
  - Public

const TCHAR * ToString ( ERejoinStatus Result )

const TCHAR * ToString ( ERejoinAttemptResult Result )



---

## RelativeBodyAnimInfo

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RelativeBodyAnimInfo

**Contents:**
- RelativeBodyAnimInfo
- Navigation
- Classes



---

## RelativeBodyAnimUtils

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RelativeBodyAnimUtils

**Contents:**
- RelativeBodyAnimUtils
- Navigation
- Classes
- Structs



---

## RelativeIKOp

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RelativeIKOp

**Contents:**
- RelativeIKOp
- Navigation
- Classes
- Structs



---

## RemoteControlCommon

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RemoteControlCommon

**Contents:**
- RemoteControlCommon
- Navigation
- Classes
- Structs
- Enums
  - Public
- Constants
- Variables
  - Public
- Functions

ENUM_CLASS_FLAGS ( ERCMask )

uint64 GetTypeHash ( const FRCPropertyContainerKey& InValue )

bool operator!= ( const FRCPropertyContainerKey& Lhs, const FRCPropertyContainerKey& Rhs )

bool operator== ( const FRCPropertyContainerKey& Lhs, const FRCPropertyContainerKey& Rhs )

TEnableIf<(TIsDerivedFrom< PropertyType, FProperty >::Value &&!std::is_same_v< PropertyType, FProperty > &&!std::is_same_v< PropertyType, FNumericProperty >)||std::is_same_v< PropertyType, FEnumProperty >, bool >::Type RemoteControlPropertyUtilities::Deserialize ( const FRCPropertyVariant& InSrc, FRCPropertyVariant& OutDst )

TEnableIf< std::is_same_v< PropertyType, FProperty >||std::is_same_v< PropertyType, FNumericProperty >, bool >::Type RemoteControlPropertyUtilities::Deserialize ( const FRCPropertyVariant& InSrc, FRCPropertyVariant& OutDst )

TEnableIf<(TIsDerivedFrom< PropertyType, FProperty >::Value &&!std::is_same_v< PropertyType, FProperty > &&!std::is_same_v< PropertyType, FNumericProperty >)||std::is_same_v< PropertyType, FEnumProperty >, bool >::Type RemoteControlPropertyUtilities::Serialize ( const FRCPropertyVariant& InSrc, FRCPropertyVariant& OutDst )

TEnableIf< std::is_same_v< PropertyType, FProperty >||std::is_same_v< PropertyType, FNumericProperty >, bool >::Type RemoteControlPropertyUtilities::Serialize ( const FRCPropertyVariant& InSrc, FRCPropertyVariant& OutDst )

SIZE_T RemoteControlTypeUtilities::GetPropertySize ( const TSharedPtr< IPropertyHandle >& InPropertyHandle )

SIZE_T RemoteControlTypeUtilities::GetPropertySize ( const FProperty* InProperty, void* InData )

static FName RemoteControlPropertyUtilities::FindLightSetterFunctionInternal ( const FProperty* Property, UClass* OwnerClass )

static FName RemoteControlPropertyUtilities::FindLightSetterFunctionInternal ( const FProperty* Property, UClass* OwnerClass )

static FProperty * RemoteControlPropertyUtilities::FindSetterArgument ( UFunction* SetterFunction, const FProperty* PropertyToModify )

static FProperty * RemoteControlPropertyUtilities::FindSetterArgument ( UFunction* SetterFunction, const FProperty* PropertyToModify )

static UFunction * RemoteControlPropertyUtilities::FindSetterFunction ( const FProperty* Property, UClass* OwnerClass )

static UFunction * RemoteControlPropertyUtilities::FindSetterFunction ( const FProperty* Property, UClass* OwnerClass )

static UFunction * RemoteControlPropertyUtilities::FindSetterFunctionInternal ( const FProperty* Property, UClass* OwnerClass )

static UFunction * RemoteControlPropertyUtilities::FindSetterFunctionInternal ( const FProperty* Property, UClass* OwnerClass )

static const FName RemoteControlPropertyUtilities::NAME_BlueprintGetter ( TEXT("BlueprintGetter") )

static const FName RemoteControlPropertyUtilities::NAME_BlueprintSetter ( TEXT("BlueprintSetter") )

static ValueType RemoteControlTypeUtilities::ClampToPropertyType ( const FNumericProperty* InProperty, ValueType& InOutValue )

static ValueType RemoteControlTypeUtilities::GetClampedValue ( Func InFunc, const PropertyType* InProperty, ValueType InValue, const TArray< FName >& InMetaKeys )

static ValueType RemoteControlTypeUtilities::GetDefaultMappingValueMax ()

static ValueType RemoteControlTypeUtilities::GetDefaultMappingValueMax ( const FProperty* InProperty )

static TSharedPtr< ValueType > RemoteControlTypeUtilities::GetDefaultMappingValueMax ( const FStructProperty* InProperty )

static ValueType RemoteControlTypeUtilities::GetDefaultMappingValueMax ( const FProperty* InProperty )

static ValueType RemoteControlTypeUtilities::GetDefaultMappingValueMin ()

static ValueType RemoteControlTypeUtilities::GetDefaultMappingValueMin ( const FProperty* InProperty )

static TSharedPtr< ValueType > RemoteControlTypeUtilities::GetDefaultMappingValueMin ( const FStructProperty* InProperty )

static ValueType RemoteControlTypeUtilities::GetDefaultMappingValueMin ( const FProperty* InProperty )

static ValueType RemoteControlTypeUtilities::GetDefaultRangeValueMax ()

static ValueType RemoteControlTypeUtilities::GetDefaultRangeValueMax ( const FProperty* InProperty )

static ValueType RemoteControlTypeUtilities::GetDefaultRangeValueMax ( const FProperty* InProperty )

static ValueType RemoteControlTypeUtilities::GetDefaultRangeValueMin ()

static ValueType RemoteControlTypeUtilities::GetDefaultRangeValueMin ( const FProperty* InProperty )

static ValueType RemoteControlTypeUtilities::GetDefaultRangeValueMin ( const PropertyType* InProperty )

static ValueType RemoteControlTypeUtilities::GetMetadataValue ( const PropertyType* InProperty, const FName& InKey, const ValueType& InDefaultValue )

static bool RemoteControlTypeUtilities::IsSupportedMappingType ( const PropertyType* InProperty )

static bool RemoteControlTypeUtilities::IsSupportedRangeType ( const PropertyType* InProperty )



---

## RemoteControlComponents

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RemoteControlComponents

**Contents:**
- RemoteControlComponents
- Navigation
- Classes
- Structs



---

## RemoteControlInterception

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RemoteControlInterception

**Contents:**
- RemoteControlInterception
- Navigation
- Structs
- Interfaces
- Enums
  - Public



---

## RemoteControlLogic

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RemoteControlLogic

**Contents:**
- RemoteControlLogic
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Constants
- Variables
  - Public

UTexture2D * UE::RCCustomBindActionUtilities::LoadTextureFromPath ( const FString& InPath )

void UE::RCCustomBindActionUtilities::SetTexturePropertyFromPath ( const TSharedRef< FRemoteControlProperty >& InRemoteControlEntityAsProperty, const FString& InPath )

bool UE::RCCustomControllers::CustomControllerExecutesOnLoad ( const URCVirtualPropertyBase* InController )

bool UE::RCCustomControllers::CustomControllerExecutesOnLoad ( const FName& InCustomControllerTypeName )

bool UE::RCCustomControllers::GetControllersOfEntity ( const URemoteControlPreset* InRemoteControlPreset, const FGuid& InEntity, TSet< const URCVirtualPropertyBase* >& OutControllers )

TMap< FName, FString > UE::RCCustomControllers::GetCustomControllerMetaData ( const FString& InCustomControllerTypeName )

EPropertyBagPropertyType UE::RCCustomControllers::GetCustomControllerType ( const FName& InCustomControllerTypeName )

EPropertyBagPropertyType UE::RCCustomControllers::GetCustomControllerType ( const FString& InCustomControllerTypeName )

FString UE::RCCustomControllers::GetCustomControllerTypeName ( const URCVirtualPropertyBase* InController )

bool UE::RCCustomControllers::GetEntitiesControlledByController ( const URemoteControlPreset* InRemoteControlPreset, const URCVirtualPropertyBase* InVirtualProperty, TSet< FGuid >& OutEntityIds )

FName UE::RCCustomControllers::GetUniqueNameForController ( const URCVirtualPropertyInContainer* InController )

bool UE::RCCustomControllers::IsCustomController ( const URCVirtualPropertyBase* InController )

bool UE::RCCustomControllers::IsValidCustomController ( const FName& InCustomControllerTypeName )



---

## RemoteControlProtocolDMX

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RemoteControlProtocolDMX

**Contents:**
- RemoteControlProtocolDMX
- Navigation
- Classes
- Structs



---

## RemoteControlProtocolMIDI

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RemoteControlProtocolMIDI

**Contents:**
- RemoteControlProtocolMIDI
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

uint64 GetTypeHash ( const FRemoteControlMIDIDevice& InValue )

bool operator!= ( const FRemoteControlMIDIDevice& Lhs, const FRemoteControlMIDIDevice& Rhs )

bool operator== ( const FRemoteControlMIDIDevice& Lhs, const FRemoteControlMIDIDevice& Rhs )



---

## RemoteControlProtocolWidgets

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RemoteControlProtocolWidgets

**Contents:**
- RemoteControlProtocolWidgets
- Navigation
- Classes
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

class UE_DEPRECATED (



---

## RemoteControlProtocol

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RemoteControlProtocol

**Contents:**
- RemoteControlProtocol
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants



---

## RemoteControlUI

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RemoteControlUI

**Contents:**
- RemoteControlUI
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants



---

## RemoteControlWebInterface

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RemoteControlWebInterface

**Contents:**
- RemoteControlWebInterface
- Navigation
- Classes



---

## RemoteControl

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RemoteControl

**Contents:**
- RemoteControl
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

bool operator! ( ERCModifyOperationFlags E )

ERCModifyOperationFlags operator& ( ERCModifyOperationFlags Lhs, ERCModifyOperationFlags Rhs )

ERCModifyOperationFlags & operator&= ( ERCModifyOperationFlags& Lhs, ERCModifyOperationFlags Rhs )

ERCModifyOperationFlags operator^ ( ERCModifyOperationFlags Lhs, ERCModifyOperationFlags Rhs )

ERCModifyOperationFlags & operator^= ( ERCModifyOperationFlags& Lhs, ERCModifyOperationFlags Rhs )

ERCModifyOperationFlags operator| ( ERCModifyOperationFlags Lhs, ERCModifyOperationFlags Rhs )

ERCModifyOperationFlags & operator|= ( ERCModifyOperationFlags& Lhs, ERCModifyOperationFlags Rhs )

ERCModifyOperationFlags operator~ ( ERCModifyOperationFlags E )



---

## RemoteDatabaseSupport

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RemoteDatabaseSupport

**Contents:**
- RemoteDatabaseSupport
- Navigation
- Classes
- Interfaces



---

## RemoteSession

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RemoteSession

**Contents:**
- RemoteSession
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

DECLARE_CYCLE_STAT ( TEXT("RS.ImageCaptureTime"), STAT_RSCaptureTime, STATGROUP_RemoteSession )

DECLARE_CYCLE_STAT ( TEXT("RS.ImageCompressTime"), STAT_RSCompressTime, STATGROUP_RemoteSession )

DECLARE_CYCLE_STAT ( TEXT("RS.ReceiveTime"), STAT_RSReceiveTime, STATGROUP_RemoteSession )

DECLARE_CYCLE_STAT ( TEXT("RS.WakeupWait"), STAT_RSWakeupWait, STATGROUP_RemoteSession )

DECLARE_CYCLE_STAT ( TEXT("RS.ImageDecompressTime"), STAT_RSDecompressTime, STATGROUP_RemoteSession )

DECLARE_CYCLE_STAT ( TEXT("RS.TextureUpdate"), STAT_RSTextureUpdate, STATGROUP_RemoteSession )

DECLARE_CYCLE_STAT ( TEXT("RS.TickRate"), STAT_RSTickRate, STATGROUP_RemoteSession )

DECLARE_CYCLE_STAT ( TEXT("RSReadyFrameCount"), STAT_RSNumFrames, STATGROUP_RemoteSession )

DECLARE_DWORD_ACCUMULATOR_STAT ( TEXT("RS.CapturedFrames/s"), STAT_RSCaptureCount, STATGROUP_RemoteSession )

DECLARE_DWORD_ACCUMULATOR_STAT ( TEXT("RS.SkippedFrames/s"), STAT_RSSkippedFrames, STATGROUP_RemoteSession )

DECLARE_DWORD_ACCUMULATOR_STAT ( TEXT("RS.WaitingFrames/s"), STAT_RSWaitingFrames, STATGROUP_RemoteSession )

DECLARE_DWORD_ACCUMULATOR_STAT ( TEXT("RS.DiscardedFrames/s"), STAT_RSDiscardedFrames, STATGROUP_RemoteSession )

DECLARE_DWORD_ACCUMULATOR_STAT ( TEXT("RS.MaxImageProcessTime"), STAT_RSMaxImageProcessTime, STATGROUP_RemoteSession )

void LexFromString ( ERemoteSessionChannelMode& Value, const TCHAR* String )

const TCHAR * LexToString ( ERemoteSessionChannelMode InMode )



---

## RenderDocPlugin

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RenderDocPlugin

**Contents:**
- RenderDocPlugin
- Navigation
- Classes
- Interfaces



---

## RenderGridDeveloper

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RenderGridDeveloper

**Contents:**
- RenderGridDeveloper
- Navigation
- Classes
- Structs
- Interfaces
- Constants



---

## RenderGridEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RenderGridEditor

**Contents:**
- RenderGridEditor
- Navigation
- Structs
- Interfaces
- Constants



---

## RenderGrid

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RenderGrid

**Contents:**
- RenderGrid
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants



---

## RenderTrace

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RenderTrace

**Contents:**
- RenderTrace
- Navigation
- Classes
- Interfaces
- Typedefs



---

## ReplayTracks

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ReplayTracks

**Contents:**
- ReplayTracks
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## ReplicationGraph

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ReplicationGraph

**Contents:**
- ReplicationGraph
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Variables
  - Public
- Functions

CSV_DECLARE_CATEGORY_EXTERN ( ReplicationGraphMS )

CSV_DECLARE_CATEGORY_EXTERN ( ReplicationGraphKBytes )

CSV_DECLARE_CATEGORY_EXTERN ( ReplicationGraphChannelsOpened )

CSV_DECLARE_CATEGORY_EXTERN ( ReplicationGraphNumReps )

CSV_DECLARE_CATEGORY_EXTERN ( ReplicationGraphVisibleLevels )

CSV_DECLARE_CATEGORY_EXTERN ( ReplicationGraphForcedUpdates )

CSV_DECLARE_CATEGORY_EXTERN ( ReplicationGraphCleanMS )

CSV_DECLARE_CATEGORY_EXTERN ( ReplicationGraphCleanNumReps )

CSV_DECLARE_CATEGORY_EXTERN ( ReplicationGraphRedundantMS )

ENUM_CLASS_FLAGS ( FGlobalActorReplicationInfoMap::EWarnFlag )

ENUM_CLASS_FLAGS ( FReplicationGraphCSVTracker::EActorFlags )

void ForEachClientPIEWorld ( TFunction< void(UWorld*)> Func )

UClass * GetActorRepListTypeClass ( const FActorRepListType& In )

FString GetActorRepListTypeDebugString ( const FActorRepListType& In )

bool IsActorValidForReplication ( const AActor* Actor )

bool IsActorValidForReplication ( const FActorRepListType& In )

bool IsActorValidForReplication_LogMoreInfo ( const FActorRepListType& In )

bool IsActorValidForReplicationGather ( const FActorRepListType& In )

LLM_DECLARE_TAG_API ( NetRepGraph )

void LogActorRepList ( FReplicationGraphDebugInfo& DebugInfo, FString Prefix, const FActorRepListRefView& List )

void LogMoreInfoOnIsActorValidFailure ( const FActorRepListType& In )

bool operator== ( UNetConnection* Other ) const

void PrintRepListDetails ( int32 PoolSize, int32 BlockIdx, int32 ListIdx )

void PrintRepListStats ( int32 mode )

void PrintRepListStatsAr ( int32 mode, FOutputDevice& Ar )



---

## ResonanceAudioEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ResonanceAudioEditor

**Contents:**
- ResonanceAudioEditor
- Navigation
- Interfaces



---

## ResonanceAudio

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ResonanceAudio

**Contents:**
- ResonanceAudio
- Navigation
- Classes
- Interfaces
- Enums
  - Public



---

## RewindDebuggerRuntime

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RewindDebuggerRuntime

**Contents:**
- RewindDebuggerRuntime
- Navigation
- Classes



---

## RewindDebuggerVLog

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RewindDebuggerVLog

**Contents:**
- RewindDebuggerVLog
- Navigation
- Interfaces



---

## RHITests

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RHITests

**Contents:**
- RHITests
- Navigation
- Classes
- Functions
  - Public
  - Static

bool IsZeroMem ( const void* Ptr, uint32 Size )

bool RunOnRenderThreadSynchronous ( TFunctionRef< bool(FRHICommandListImmediate&)> TestFunc )

static FString ClearValueToString ( const ValueType& ClearValue )



---

## RigLogicDeveloper

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RigLogicDeveloper

**Contents:**
- RigLogicDeveloper
- Navigation
- Classes



---

## RigLogicEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RigLogicEditor

**Contents:**
- RigLogicEditor
- Navigation
- Classes
- Structs
- Functions
  - Public

void ApplyImportUIToImportOptions ( UDNAAssetImportUI* ImportUI, FDNAAssetImportOptions& InOutImportOptions )

FDNAAssetImportOptions * GetImportOptions ( FDNAImporter* DNAImporter, UDNAAssetImportUI* ImportUI, bool bShowOptionDialog, bool bIsAutomated, const FString& FullPath, bool& OutOperationCanceled, const FString& InFilename )



---

## RigLogicLibTest

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RigLogicLibTest

**Contents:**
- RigLogicLibTest
- Navigation
- Classes



---

## RigLogicLib

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RigLogicLib

**Contents:**
- RigLogicLib
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Constants
- Functions
  - Public

bool av::operator!= ( const ArrayView< T >& lhs, const ArrayView< U >& rhs )

std::enable_ifArrayView< T >, TContainer >::value, bool >::type av::operator!= ( const ArrayView< T >& lhs, const TContainer& rhs )

std::enable_ifArrayView< T >, TContainer >::value, bool >::type av::operator!= ( const TContainer& lhs, const ArrayView< T >& rhs )

bool av::operator== ( const ArrayView< T >& lhs, const ArrayView< U >& rhs )

std::enable_ifArrayView< T >, TContainer >::value, bool >::type av::operator== ( const ArrayView< T >& lhs, const TContainer& rhs )

std::enable_ifArrayView< T >, TContainer >::value, bool >::type av::operator== ( const TContainer& lhs, const ArrayView< T >& rhs )

std::uint8_t bswap ( std::uint8_t x )

std::uint16_t bswap ( std::uint16_t x )

std::uint32_t bswap ( std::uint32_t x )

std::uint64_t bswap ( std::uint64_t x )

void bswap ( std::uint8_t* x )

void bswap ( std::uint16_t* x )

void bswap ( std::uint32_t* x )

void bswap ( std::uint64_t* x )

Vector3 dna::operator- ( Vector3 lhs, const Vector3& rhs )

Vector3 dna::operator- ( Vector3 lhs, float rhs )

bool dna::operator!= ( const Vector3& lhs, const Vector3& rhs )

Vector3 dna::operator* ( Vector3 lhs, const Vector3& rhs )

Vector3 dna::operator* ( Vector3 lhs, float rhs )

Vector3 dna::operator/ ( Vector3 lhs, const Vector3& rhs )

Vector3 dna::operator/ ( Vector3 lhs, float rhs )

DataLayer dna::operator| ( DataLayer lhs, DataLayer rhs )

Vector3 dna::operator+ ( Vector3 lhs, const Vector3& rhs )

Vector3 dna::operator+ ( Vector3 lhs, float rhs )

bool dna::operator== ( const Vector3& lhs, const Vector3& rhs )

std::uint8_t hton ( std::uint8_t x )

std::uint16_t hton ( std::uint16_t x )

std::uint32_t hton ( std::uint32_t x )

std::uint64_t hton ( std::uint64_t x )

void hton ( std::uint8_t* x )

void hton ( std::uint16_t* x )

void hton ( std::uint32_t* x )

void hton ( std::uint64_t* x )

std::uint8_t ntoh ( std::uint8_t x )

std::uint16_t ntoh ( std::uint16_t x )

std::uint32_t ntoh ( std::uint32_t x )

std::uint64_t ntoh ( std::uint64_t x )

void ntoh ( std::uint8_t* x )

void ntoh ( std::uint16_t* x )

void ntoh ( std::uint32_t* x )

void ntoh ( std::uint64_t* x )

ScopedPtr< Base, TDestroyer > pma::makeScoped ( Args&&... args )

ScopedPtr< T, TDestroyerTemplate< T > > pma::makeScoped ( Args&&... args )

ScopedPtr< T, typename DefaultInstanceDestroyer< T >::type > pma::makeScoped ( Args&&... args )

bool pma::operator!= ( const PolyAllocator< T, TAlignment, TDefaultMemoryResource >& lhs, const PolyAllocator< U, UAlignment, UDefaultMemoryResource >& rhs )

bool pma::operator== ( const PolyAllocator< T, TAlignment, TDefaultMemoryResource >& lhs, const PolyAllocator< U, UAlignment, UDefaultMemoryResource >& rhs )

bool sc::operator!= ( const StatusCode& lhs, const StatusCode& rhs )

bool sc::operator== ( const StatusCode& lhs, const StatusCode& rhs )

mat< L, L, T > tdm::affine::scale ( const vec< L, T >& factors )

mat< L, L, T > tdm::affine::scale ( T factor )

mat< L, L, T > tdm::affine::scale ( const mat< L, L, T >& m, const vec< L, T >& factors )

mat< L, L, T > tdm::affine::scale ( const mat< L, L, T >& m, T factor )

fdeg tdm::ang_literals::operator""_fdeg ( long double angle )

frad tdm::ang_literals::operator""_frad ( long double angle )

mat< R, C, T > tdm::applied ( const mat< R, C, T >& lhs, F func )

vec< L, T > tdm::applied ( const vec< L, T >& lhs, F func )

quat< T > tdm::conjugate ( const quat< T >& q )

vec3< T > tdm::cross ( const vec3< T >& lhs, const vec3< T >& rhs )

std::enable_if< std::is_floating_point< T >::value, T >::type tdm::degrees ( T radians )

T tdm::determinant ( const mat< N, N, T >& m )

T tdm::dot ( const vec< L, T >& lhs, const vec< L, T >& rhs )

T tdm::dot ( const quat< T >& q1, const quat< T >& q2 )

std::enable_if< std::is_floating_point< T >::value, T >::type tdm::fastasin ( T value )

mat< N, N, T > tdm::impl::adjoint ( const mat< N, N, T >& m )

T tdm::impl::determinant ( const mat< N, N, T >& m, dim_t dimensions )

quat< T > tdm::impl::euler2quat ( const rad3< T >& rot, rot_seq order )

void tdm::impl::minor ( const mat< N, N, T >& input, dim_t dimensions, dim_t i, dim_t j, mat< N, N, T >& output )

rad3< T > tdm::impl::quat2euler ( const quat< T >& q, rot_seq order )

quat< T > tdm::inverse ( const quat< T >& q )

mat< N, N, T > tdm::inverse ( const mat< N, N, T >& m )

std::enable_if< std::is_floating_point< T >::value, T >::type tdm::length ( const vec< L, T >& v )

std::enable_if< std::is_floating_point< T >::value, T >::type tdm::length ( const quat< T >& q )

quat< T > tdm::lerp ( const quat< T >& q1, const quat< T >& q2, T t )

bool tdm::lu::decompose ( mat< N, N, T >& a, vec< N, dim_t >& permute )

mat< N, N, T > tdm::lu::inverse ( mat< N, N, T > m )

void tdm::lu::substitute ( const mat< N, N, T >& a, const vec< N, dim_t >& permute, vec< N, T >& b )

vec< L, T > tdm::negate ( vec< L, T > v )

mat< R, C, T > tdm::negate ( mat< R, C, T > m )

quat< T > tdm::negate ( quat< T > q )

std::enable_if< std::is_floating_point< T >::value, vec< L, T > >::type tdm::normalize ( vec< L, T > v )

std::enable_if< std::is_floating_point< T >::value, quat< T > >::type tdm::normalize ( quat< T > q )

mat< R, C, T > tdm::operator- ( const mat< R, C, T >& m )

vec< L, T > tdm::operator- ( vec< L, T > v )

ang< T, TUnit > tdm::operator- ( const ang< T, TUnit >& lhs, const ang< T, TUnit >& rhs )

mat< R, C, T > tdm::operator- ( const mat< R, C, T >& lhs, T rhs )

mat< R, C, T > tdm::operator- ( T lhs, const mat< R, C, T >& rhs )

mat< R, C, T > tdm::operator- ( const mat< R, C, T >& lhs, const mat< R, C, T >& rhs )

quat< T > tdm::operator- ( const quat< T >& lhs, const quat< T >& rhs )

vec< L, T > tdm::operator- ( const vec< L, T >& lhs, const vec< L, U >& rhs )

vec< L, T > tdm::operator- ( const vec< L, T >& lhs, U rhs )

vec< L, T > tdm::operator- ( T lhs, const vec< L, U >& rhs )

bool tdm::operator!= ( const ang< T, TUnit >& lhs, const ang< T, TUnit >& rhs )

bool tdm::operator!= ( const mat< R, C, T >& lhs, const mat< R, C, T >& rhs )

bool tdm::operator!= ( const quat< T >& lhs, const quat< T >& rhs )

bool tdm::operator!= ( const vec< L, T >& lhs, const vec< L, T >& rhs )

ang< T, TUnit > tdm::operator* ( const ang< T, TUnit >& lhs, T rhs )

ang< T, TUnit > tdm::operator* ( T lhs, const ang< T, TUnit >& rhs )

mat< R, C, T > tdm::operator* ( const mat< R, C, T >& lhs, T rhs )

mat< R, C, T > tdm::operator* ( T lhs, const mat< R, C, T >& rhs )

mat< R, C, T >::row_type tdm::operator* ( const typename mat< R, C, T >::column_type& lhs, const mat< R, C, T >& rhs )

mat< R, C, T >::column_type tdm::operator* ( const mat< R, C, T >& lhs, const typename mat< R, C, T >::row_type& rhs )

mat< R, C, T > tdm::operator* ( const mat< R, S, T >& lhs, const mat< S, C, T >& rhs )

quat< T > tdm::operator* ( const quat< T >& lhs, const quat< T >& rhs )

quat< T > tdm::operator* ( const quat< T >& lhs, T rhs )

quat< T > tdm::operator* ( T lhs, const quat< T >& rhs )

vec< L, T > tdm::operator* ( const vec< L, T >& lhs, const vec< L, U >& rhs )

std::enable_if< std::is_arithmetic< U >::value, vec< L, T > >::type tdm::operator* ( const vec< L, T >& lhs, U rhs )

std::enable_if< std::is_arithmetic< T >::value, vec< L, T > >::type tdm::operator* ( T lhs, const vec< L, U >& rhs )

ang< T, TUnit > tdm::operator/ ( const ang< T, TUnit >& lhs, T rhs )

mat< R, C, T > tdm::operator/ ( const mat< R, C, T >& lhs, T rhs )

mat< R, C, T > tdm::operator/ ( T lhs, const mat< R, C, T >& rhs )

mat< R, C, T >::row_type tdm::operator/ ( const typename mat< R, C, T >::column_type& lhs, const mat< R, C, T >& rhs )

mat< R, C, T >::column_type tdm::operator/ ( const mat< R, C, T >& lhs, const typename mat< R, C, T >::row_type& rhs )

mat< R, C, T > tdm::operator/ ( const mat< R, C, T >& lhs, const mat< R, C, T >& rhs )

quat< T > tdm::operator/ ( const quat< T >& lhs, T rhs )

quat< T > tdm::operator/ ( T lhs, const quat< T >& rhs )

vec< L, T > tdm::operator/ ( const vec< L, T >& lhs, const vec< L, U >& rhs )

std::enable_if< std::is_arithmetic< U >::value, vec< L, T > >::type tdm::operator/ ( const vec< L, T >& lhs, U rhs )

std::enable_if< std::is_arithmetic< T >::value, vec< L, T > >::type tdm::operator/ ( T lhs, const vec< L, U >& rhs )

mat< R, C, T > tdm::operator+ ( const mat< R, C, T >& m )

vec< L, T > tdm::operator+ ( const vec< L, T >& v )

ang< T, TUnit > tdm::operator+ ( const ang< T, TUnit >& lhs, const ang< T, TUnit >& rhs )

mat< R, C, T > tdm::operator+ ( const mat< R, C, T >& lhs, T rhs )

mat< R, C, T > tdm::operator+ ( T lhs, const mat< R, C, T >& rhs )

mat< R, C, T > tdm::operator+ ( const mat< R, C, T >& lhs, const mat< R, C, T >& rhs )

quat< T > tdm::operator+ ( const quat< T >& lhs, const quat< T >& rhs )

vec< L, T > tdm::operator+ ( const vec< L, T >& lhs, const vec< L, U >& rhs )

vec< L, T > tdm::operator+ ( const vec< L, T >& lhs, U rhs )

vec< L, T > tdm::operator+ ( T lhs, const vec< L, U >& rhs )

bool tdm::operator== ( const ang< T, TUnit >& lhs, const ang< T, TUnit >& rhs )

bool tdm::operator== ( const mat< R, C, T >& lhs, const mat< R, C, T >& rhs )

bool tdm::operator== ( const quat< T >& lhs, const quat< T >& rhs )

bool tdm::operator== ( const vec< L, T >& lhs, const vec< L, T >& rhs )

mat4< T > tdm::projective::rotate ( const rad3< T >& rotation, handedness h )

mat4< T > tdm::projective::rotate ( const vec3< T >& axis, rad< T > angle, handedness h )

mat4< T > tdm::projective::rotate ( const mat4< T >& m, const rad3< T >& rotation, handedness h )

mat4< T > tdm::projective::rotate ( const mat4< T >& m, const vec3< T >& axis, rad< T > angle, handedness h )

mat4< T > tdm::projective::rotate ( rad< T > x, rad< T > y, rad< T > z, handedness h )

mat4< T > tdm::projective::rotate ( const mat4< T >& m, rad< T > x, rad< T > y, rad< T > z, handedness h )

mat< L+1, L+1, T > tdm::projective::scale ( const vec< L, T >& factors )

mat< L+1, L+1, T > tdm::projective::scale ( T factor )

mat< L+1, L+1, T > tdm::projective::scale ( const mat< L+1, L+1, T >& m, const vec< L, T >& factors )

mat< L, L, T > tdm::projective::scale ( const mat< L, L, T >& m, T factor )

mat< L+1, L+1, T > tdm::projective::translate ( const vec< L, T >& position )

mat< L+1, L+1, T > tdm::projective::translate ( const mat< L+1, L+1, T >& m, const vec< L, T >& position )

std::enable_if< std::is_floating_point< T >::value, T >::type tdm::radians ( T degrees )

mat4< T > tdm::rotate ( const rad3< T >& rotation, handedness h )

mat4< T > tdm::rotate ( const vec3< T >& axis, rad< T > angle, handedness h )

mat4< T > tdm::rotate ( const mat4< T >& m, const rad3< T >& rotation, handedness h )

mat4< T > tdm::rotate ( const mat4< T >& m, const vec3< T >& axis, rad< T > angle, handedness h )

mat4< T > tdm::rotate ( rad< T > x, rad< T > y, rad< T > z, handedness h )

mat4< T > tdm::rotate ( const mat4< T >& m, rad< T > x, rad< T > y, rad< T > z, handedness h )

mat< L+1, L+1, T > tdm::scale ( const vec< L, T >& factors )

mat< L+1, L+1, T > tdm::scale ( T factor )

mat< L+1, L+1, T > tdm::scale ( const mat< L+1, L+1, T >& m, const vec< L, T >& factors )

mat< L, L, T > tdm::scale ( const mat< L, L, T >& m, T factor )

quat< T > tdm::slerp ( const quat< T >& q1, const quat< T >& q2, T t )

T tdm::trace ( const mat< N, N, T >& m )

mat< L+1, L+1, T > tdm::translate ( const vec< L, T >& position )

mat< L+1, L+1, T > tdm::translate ( const mat< L+1, L+1, T >& m, const vec< L, T >& position )

mat< C, R, T > tdm::transpose ( const mat< R, C, T >& m )

std::size_t terse::base64decode ( std::size_t size )

std::size_t terse::base64decode ( char* destination, const char* source, std::size_t size )

std::size_t terse::base64encode ( std::size_t size )

std::size_t terse::base64encode ( char* destination, const char* source, std::size_t size )

void terse::hostToNetwork ( T& value )

void terse::hostToNetwork128 ( T* values )

void terse::networkToHost ( T& value )

void terse::networkToHost128 ( T* values )

ArchiveOffset< TOffset >::Proxy terse::proxy ( ArchiveOffset< TOffset >& offset )

ArchiveSize< TSize, TOffset >::Proxy terse::proxy ( ArchiveSize< TSize, TOffset >& size, Anchor< TOffset >& base )

Transparent< T > terse::transparent ( T& data )

Versioned< T, V > terse::versioned ( T& dest, V )

trimd::attribute ( (always_inline) )

T256< T128 > trimd::fallback::abs ( const T256< T128 >& rhs )

T256< T128 > trimd::fallback::andnot ( const T256< T128 >& lhs, const T256< T128 >& rhs )

T256< T128 > trimd::fallback::operator- ( const T256< T128 >& lhs, const T256< T128 >& rhs )

T256< T128 > trimd::fallback::operator!= ( const T256< T128 >& lhs, const T256< T128 >& rhs )

T256< T128 > trimd::fallback::operator& ( const T256< T128 >& lhs, const T256< T128 >& rhs )

T256< T128 > trimd::fallback::operator* ( const T256< T128 >& lhs, const T256< T128 >& rhs )

T256< T128 > trimd::fallback::operator/ ( const T256< T128 >& lhs, const T256< T128 >& rhs )

T256< T128 > trimd::fallback::operator^ ( const T256< T128 >& lhs, const T256< T128 >& rhs )

T256< T128 > trimd::fallback::operator| ( const T256< T128 >& lhs, const T256< T128 >& rhs )

T256< T128 > trimd::fallback::operator~ ( const T256< T128 >& rhs )

T256< T128 > trimd::fallback::operator+ ( const T256< T128 >& lhs, const T256< T128 >& rhs )

T256< T128 > trimd::fallback::operator== ( const T256< T128 >& lhs, const T256< T128 >& rhs )

T256< T128 > trimd::fallback::operator> ( const T256< T128 >& lhs, const T256< T128 >& rhs )

T256< T128 > trimd::fallback::operator>= ( const T256< T128 >& lhs, const T256< T128 >& rhs )

T256< T128 > trimd::fallback::rsqrt ( const T256< T128 >& rhs )

void trimd::fallback::transpose ( T256< T128 >& row0, T256< T128 >& row1, T256< T128 >& row2, T256< T128 >& row3, T256< T128 >& row4, T256< T128 >& row5, T256< T128 >& row6, T256< T128 >& row7 )

CPUFeatures trimd::getCPUFeatures()

T128< T > trimd::scalar::abs ( const T128< T >& rhs )

T128< T > trimd::scalar::andnot ( const T128< T >& lhs, const T128< T >& rhs )

T128< T > trimd::scalar::operator- ( const T128< T >& lhs, const T128< T >& rhs )

T128< T > trimd::scalar::operator!= ( const T128< T >& lhs, const T128< T >& rhs )

T128< T > trimd::scalar::operator& ( const T128< T >& lhs, const T128< T >& rhs )

T128< T > trimd::scalar::operator* ( const T128< T >& lhs, const T128< T >& rhs )

T128< T > trimd::scalar::operator/ ( const T128< T >& lhs, const T128< T >& rhs )

T128< T > trimd::scalar::operator^ ( const T128< T >& lhs, const T128< T >& rhs )

T128< T > trimd::scalar::operator| ( const T128< T >& lhs, const T128< T >& rhs )

T128< T > trimd::scalar::operator~ ( const T128< T >& rhs )

T128< T > trimd::scalar::operator+ ( const T128< T >& lhs, const T128< T >& rhs )

T128< T > trimd::scalar::operator== ( const T128< T >& lhs, const T128< T >& rhs )

T128< T > trimd::scalar::operator> ( const T128< T >& lhs, const T128< T >& rhs )

T128< T > trimd::scalar::operator>= ( const T128< T >& lhs, const T128< T >& rhs )

T128< T > trimd::scalar::rsqrt ( const T128< T >& rhs )

void trimd::scalar::transpose ( T128< T >& row0, T128< T >& row1, T128< T >& row2, T128< T >& row3 )

static std::uint16_t bswap16 ( std::uint16_t x )

static void bswap16x8 ( std::uint16_t* source )

static std::uint32_t bswap32 ( std::uint32_t x )

static void bswap32x4 ( std::uint32_t* source )

static std::uint64_t bswap64 ( std::uint64_t x )

static void bswap64x2 ( std::uint64_t* source )

static true_sink< decltype(load(std::declval< T & >(), std::declval< T & >()))> terse::traits::test_load_function ( std::int32_t )

static std::false_type terse::traits::test_load_function ( std::uint32_t )

static true_sink< decltype(std::declval< T >().load(std::declval< T & >()))> terse::traits::test_load_member ( std::int32_t )

static std::false_type terse::traits::test_load_member ( std::uint32_t )

static true_sink< decltype(std::declval< TContainer >().push_back(std::declval< typename TContainer::value_type >()))> terse::traits::test_push_back_member ( std::int32_t )

static std::false_type terse::traits::test_push_back_member ( std::uint32_t )

static true_sink< decltype(std::declval< TContainer >().reserve(0u))> terse::traits::test_reserve_member ( std::int32_t )

static std::false_type terse::traits::test_reserve_member ( std::uint32_t )

static true_sink< decltype(save(std::declval< T & >(), std::declval< T & >()))> terse::traits::test_save_function ( std::int32_t )

static std::false_type terse::traits::test_save_function ( std::uint32_t )

static true_sink< decltype(std::declval< T >().save(std::declval< T & >()))> terse::traits::test_save_member ( std::int32_t )

static std::false_type terse::traits::test_save_member ( std::uint32_t )

static true_sink< decltype(serialize(std::declval< T & >(), std::declval< T & >()))> terse::traits::test_serialize_function ( std::int32_t )

static std::false_type terse::traits::test_serialize_function ( std::uint32_t )

static true_sink< decltype(std::declval< T >().serialize(std::declval< T & >()))> terse::traits::test_serialize_member ( std::int32_t )

static std::false_type terse::traits::test_serialize_member ( std::uint32_t )

static true_sink< decltype(load(std::declval< T & >(), V{}, std::declval< T & >())) > terse::traits::test_versioned_load_function ( std::int32_t )

static std::false_type terse::traits::test_versioned_load_function ( std::uint32_t )

static true_sink< decltype(std::declval< T >().load(std::declval< T & >(), V{})) > terse::traits::test_versioned_load_member ( std::int32_t )

static std::false_type terse::traits::test_versioned_load_member ( std::uint32_t )

static true_sink< decltype(save(std::declval< T & >(), V{}, std::declval< T & >())) > terse::traits::test_versioned_save_function ( std::int32_t )

static std::false_type terse::traits::test_versioned_save_function ( std::uint32_t )

static true_sink< decltype(std::declval< T >().save(std::declval< T & >(), V{})) > terse::traits::test_versioned_save_member ( std::int32_t )

static std::false_type terse::traits::test_versioned_save_member ( std::uint32_t )

static true_sink< decltype(serialize(std::declval< T & >(), V{}, std::declval< T & >())) > terse::traits::test_versioned_serialize_function ( std::int32_t )

static std::false_type terse::traits::test_versioned_serialize_function ( std::uint32_t )

static true_sink< decltype(std::declval< T >().serialize(std::declval< T & >(), V{})) > terse::traits::test_versioned_serialize_member ( std::int32_t )

static std::false_type terse::traits::test_versioned_serialize_member ( std::uint32_t )



---

## RigLogicModule

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RigLogicModule

**Contents:**
- RigLogicModule
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

dna::DataLayer CalculateDNADataLayerBitmask ( EDNADataLayer Layer )

TObjectPtr< class UDNAAsset > GetDNAAssetFromFile ( const FString& InFilePath, UObject* InOuter, EDNADataLayer InLayer )

bool operator! ( EDNADataLayer E )

EDNADataLayer operator& ( EDNADataLayer Lhs, EDNADataLayer Rhs )

EDNADataLayer & operator&= ( EDNADataLayer& Lhs, EDNADataLayer Rhs )

EDNADataLayer operator^ ( EDNADataLayer Lhs, EDNADataLayer Rhs )

EDNADataLayer & operator^= ( EDNADataLayer& Lhs, EDNADataLayer Rhs )

EDNADataLayer operator| ( EDNADataLayer Lhs, EDNADataLayer Rhs )

EDNADataLayer & operator|= ( EDNADataLayer& Lhs, EDNADataLayer Rhs )

EDNADataLayer operator~ ( EDNADataLayer E )

TSharedPtr< IDNAReader > ReadDNAFromBuffer ( TArray< uint8 >* DNABuffer, EDNADataLayer Layer, uint16_t MaxLOD )

TSharedPtr< IDNAReader > ReadDNAFromBuffer ( TArray< uint8 >* DNABuffer, EDNADataLayer Layer, TArrayView< uint16_t > LODs )

TSharedPtr< IDNAReader > ReadDNAFromFile ( const FString& Path, EDNADataLayer Layer, uint16_t MaxLOD )

TSharedPtr< IDNAReader > ReadDNAFromFile ( const FString& Path, EDNADataLayer Layer, TArrayView< uint16_t > LODs )

TArray< uint8 > ReadStreamFromDNA ( const IDNAReader* Reader, EDNADataLayer Layer )

void WriteDNAToFile ( const IDNAReader* Reader, EDNADataLayer Layer, const FString& Path )



---

## RigLogicMutableEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RigLogicMutableEditor

**Contents:**
- RigLogicMutableEditor
- Navigation
- Classes



---

## RigLogicMutable

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RigLogicMutable

**Contents:**
- RigLogicMutable
- Navigation
- Classes
- Structs



---

## RigLogicUAFUncookedOnly

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RigLogicUAFUncookedOnly

**Contents:**
- RigLogicUAFUncookedOnly
- Navigation
- Classes



---

## RigLogicUAF

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RigLogicUAF

**Contents:**
- RigLogicUAF
- Navigation
- Classes
- Structs



---

## RigMapperDeveloper

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RigMapperDeveloper

**Contents:**
- RigMapperDeveloper
- Navigation
- Classes



---

## RigMapperEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RigMapperEditor

**Contents:**
- RigMapperEditor
- Navigation
- Classes



---

## RigMapperOp

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RigMapperOp

**Contents:**
- RigMapperOp
- Navigation
- Classes
- Structs



---

## RigMapper

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RigMapper

**Contents:**
- RigMapper
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## RigVMDeveloper

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RigVMDeveloper

**Contents:**
- RigVMDeveloper
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

uint32 GetTypeHash ( const FRigVMPinInfoArray& InPins )

FString RigVMPythonUtils::EnumValueToPythonString ( int64 Value )

FString RigVMPythonUtils::EnumValueToPythonString ( UEnum* Enum, int64 Value )

FString RigVMPythonUtils::LinearColorToPythonString ( const FLinearColor& Color )

void RigVMPythonUtils::Print ( const FString& BlueprintTitle, const FString& InMessage )

void RigVMPythonUtils::PrintPythonContext ( const FString& InBlueprintName )

FString RigVMPythonUtils::PythonizeName ( FStringView InName, const EPythonizeNameCase InNameCase )

FString RigVMPythonUtils::TransformToPythonString ( const FTransform& Transform )

FString RigVMPythonUtils::Vector2DToPythonString ( const FVector2D& Vector )



---

## RigVMEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RigVMEditor

**Contents:**
- RigVMEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

bool operator! ( FRigVMActionMenuBuilder::EConfigFlags E )

FRigVMActionMenuBuilder::EConfigFlags operator& ( FRigVMActionMenuBuilder::EConfigFlags Lhs, FRigVMActionMenuBuilder::EConfigFlags Rhs )

FRigVMActionMenuBuilder::EConfigFlags & operator&= ( FRigVMActionMenuBuilder::EConfigFlags& Lhs, FRigVMActionMenuBuilder::EConfigFlags Rhs )

FRigVMActionMenuBuilder::EConfigFlags operator^ ( FRigVMActionMenuBuilder::EConfigFlags Lhs, FRigVMActionMenuBuilder::EConfigFlags Rhs )

FRigVMActionMenuBuilder::EConfigFlags & operator^= ( FRigVMActionMenuBuilder::EConfigFlags& Lhs, FRigVMActionMenuBuilder::EConfigFlags Rhs )

FRigVMActionMenuBuilder::EConfigFlags operator| ( FRigVMActionMenuBuilder::EConfigFlags Lhs, FRigVMActionMenuBuilder::EConfigFlags Rhs )

FRigVMActionMenuBuilder::EConfigFlags & operator|= ( FRigVMActionMenuBuilder::EConfigFlags& Lhs, FRigVMActionMenuBuilder::EConfigFlags Rhs )

FRigVMActionMenuBuilder::EConfigFlags operator~ ( FRigVMActionMenuBuilder::EConfigFlags E )

void RigVMFindReferencesHelpers::ExpandAllChildren ( FRigVMSearchResult InTreeNode, TSharedPtr< STreeView< FRigVMSearchResult > > InTreeView )

FString RigVMFindReferencesHelpers::GetPinTypeAsString ( const FEdGraphPinType& InPinType )

bool RigVMFindReferencesHelpers::ParsePinType ( FText InKey, FText InValue, FEdGraphPinType& InOutPinType )



---

## RigVM

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RigVM

**Contents:**
- RigVM
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

void RigVM::ZeroPaddedMemory ( void* InFirstMember, const void* InSecondMember )

void RigVMCopy ( void* InTargetPtr, const void* InSourcePtr, int32 InCount )

bool RigVMCore::SupportsUInterfaces()

bool RigVMCore::SupportsUObjects()

void RigVMDestroy ( void* InPtr, int32 InCount )

void RigVMInitialize ( void* InPtr, int32 InCount )

uint32 RigVMPropertyUtils::GetPropertyHashFast ( const FProperty* InProperty, const uint8* InMemory, EPropertyPointerType InContainerType )

uint32 RigVMPropertyUtils::GetPropertyHashStable ( const FProperty* InProperty, const uint8* InMemory, EPropertyPointerType InContainerType )

void RigVMPropertyUtils::GetTypeFromProperty ( const FProperty* InProperty, FName& OutTypeName, UObject*& OutTypeObject )

FString RigVMStringUtils::JoinDefaultValue ( const TArray< FString >& InParts )

FString RigVMStringUtils::JoinNodePath ( const TArray< FString >& InParts )

FString RigVMStringUtils::JoinNodePath ( const FString& Left, const FString& Right )

FString RigVMStringUtils::JoinPinPath ( const TArray< FString >& InParts )

FString RigVMStringUtils::JoinPinPath ( const FString& Left, const FString& Right )

FString RigVMStringUtils::JoinStrings ( const TArray< FString >& InStrings, const TCHAR* InSeparator, const TCHAR* InPrefix, const TCHAR* InSuffix )

FString RigVMStringUtils::JoinStrings ( const TArrayView< FString >& InStrings, const TCHAR* InSeparator, const TCHAR* InPrefix, const TCHAR* InSuffix )

FString RigVMStringUtils::JoinStrings ( const FString& InStringA, const FString& InStringB, const TCHAR* InSeparator, const TCHAR* InPrefix, const TCHAR* InSuffix )

FString RigVMStringUtils::JoinStringsConst ( const TArrayView< const FString >& InStrings, const TCHAR* InSeparator, const TCHAR* InPrefix, const TCHAR* InSuffix )

FString RigVMStringUtils::MakeTemplateNotation ( const FString& InTemplateName, const TArray< FString >& InArgumentNotations )

void RigVMStringUtils::SanitizeName ( FString& InOutName, bool bAllowPeriod, bool bAllowSpace, int32 InMaxNameLength )

TArray< FString > RigVMStringUtils::SplitDefaultValue ( const FString& InDefaultValue )

bool RigVMStringUtils::SplitNodePath ( const FString& InNodePath, TArray< FString >& Parts )

bool RigVMStringUtils::SplitNodePathAtEnd ( const FString& InNodePath, FString& Left, FString& RightMost )

bool RigVMStringUtils::SplitNodePathAtStart ( const FString& InNodePath, FString& LeftMost, FString& Right )

bool RigVMStringUtils::SplitPinPath ( const FString& InPinPath, TArray< FString >& Parts )

bool RigVMStringUtils::SplitPinPathAtEnd ( const FString& InPinPath, FString& Left, FString& RightMost )

bool RigVMStringUtils::SplitPinPathAtStart ( const FString& InPinPath, FString& LeftMost, FString& Right )

bool RigVMStringUtils::SplitString ( const FString& InString, const TCHAR* InSeparator, TArray< FString >& InOutParts )

FString RigVMTypeUtils::ArrayTypeFromBaseType ( const FString& InCPPType )

FString RigVMTypeUtils::BaseTypeFromArrayType ( const FString& InCPPType )

const FLazyName RigVMTypeUtils::BoolArrayTypeName ( BoolArrayType )

const FLazyName RigVMTypeUtils::BoolTypeName ( BoolType )

FString RigVMTypeUtils::CPPTypeFromEnum ( const UEnum* InEnum )

const FLazyName RigVMTypeUtils::DoubleArrayTypeName ( DoubleArrayType )

const FLazyName RigVMTypeUtils::DoubleTypeName ( DoubleType )

FRigVMExternalVariable RigVMTypeUtils::ExternalVariableFromBPVariableDescription ( const FBPVariableDescription& InVariableDescription )

FRigVMExternalVariable RigVMTypeUtils::ExternalVariableFromBPVariableDescription ( const FBPVariableDescription& InVariableDescription, void* Container )

FRigVMExternalVariable RigVMTypeUtils::ExternalVariableFromCPPType ( const FName& InName, const FString& InCPPType, UObject* InCPPTypeObject, bool bInPublic, bool bInReadonly )

FRigVMExternalVariable RigVMTypeUtils::ExternalVariableFromCPPTypePath ( const FName& InName, const FString& InCPPTypePath, bool bInPublic, bool bInReadonly )

FRigVMExternalVariable RigVMTypeUtils::ExternalVariableFromPinType ( const FName& InName, const FEdGraphPinType& InPinType, bool bInPublic, bool bInReadonly )

const FLazyName RigVMTypeUtils::FloatArrayTypeName ( FloatArrayType )

const FLazyName RigVMTypeUtils::FloatTypeName ( FloatType )

const FLazyName RigVMTypeUtils::FNameArrayTypeName ( FNameArrayType )

const FLazyName RigVMTypeUtils::FNameTypeName ( FNameType )

const FLazyName RigVMTypeUtils::FStringArrayTypeName ( FStringArrayType )

const FLazyName RigVMTypeUtils::FStringTypeName ( FStringType )

const FLazyName RigVMTypeUtils::FTextTypeName ( FTextType )

TArray< FRigVMExternalVariableDef > RigVMTypeUtils::GetExternalVariableDefs ( const TArray< FRigVMExternalVariable >& ExternalVariables )

FString RigVMTypeUtils::GetUniqueStructTypeName ( const FGuid& InStructGuid )

FString RigVMTypeUtils::GetUniqueStructTypeName ( const UScriptStruct* InScriptStruct )

const FLazyName RigVMTypeUtils::Int32ArrayTypeName ( Int32ArrayType )

const FLazyName RigVMTypeUtils::Int32TypeName ( Int32Type )

const FLazyName RigVMTypeUtils::Int64TypeName ( Int64Type )

const FLazyName RigVMTypeUtils::IntTypeName ( IntType )

bool RigVMTypeUtils::IsArrayType ( const FString& InCPPType )

bool RigVMTypeUtils::IsInterfaceType ( const FString& InCPPType )

bool RigVMTypeUtils::IsUClassType ( const FString& InCPPType )

bool RigVMTypeUtils::IsUObjectType ( const FString& InCPPType )

const FLazyName RigVMTypeUtils::UInt32ArrayTypeName ( UInt32ArrayType )

const FLazyName RigVMTypeUtils::UInt32TypeName ( UInt32Type )

const FLazyName RigVMTypeUtils::UInt64TypeName ( UInt64Type )

const FLazyName RigVMTypeUtils::UInt8ArrayTypeName ( UInt8ArrayType )

const FLazyName RigVMTypeUtils::UInt8TypeName ( UInt8Type )

UObject * RigVMTypeUtils::UserDefinedTypeFromCPPType ( FString& InOutCPPType, const FRigVMUserDefinedTypeResolver* InTypeResolver )

static bool RigVMTypeUtils::AreCompatible ( const FProperty* InSourceProperty, const FProperty* InTargetProperty )

static void RigVMTypeUtils::CleanupCPPType ( FString& CPPType )

static FString RigVMTypeUtils::CPPTypeFromObject ( const UObject* InCPPTypeObject, EClassArgType InClassArgType )

static UObject * RigVMTypeUtils::FindObjectFromCPPTypeObjectPath ( const FString& InObjectPath )

static T * RigVMTypeUtils::FindObjectFromCPPTypeObjectPath ( const FString& InObjectPath )

static UObject * RigVMTypeUtils::FindObjectGlobally ( const TCHAR* InObjectName, bool bUseRedirector )

static bool RigVMTypeUtils::FixCPPTypeAndObject ( FString& InOutCPPType, TObjectPtr< UObject >& InOutCPPTypeObject, const FRigVMUserDefinedTypeResolver* InResolvalInfo )

static FString RigVMTypeUtils::GetCPPTypeFromProperty ( const FProperty* InProperty )

static const FString & RigVMTypeUtils::GetWildCardArrayCPPType()

static const FLazyName & RigVMTypeUtils::GetWildCardArrayCPPTypeName()

static const FString & RigVMTypeUtils::GetWildCardCPPType()

static const FLazyName & RigVMTypeUtils::GetWildCardCPPTypeName()

static UScriptStruct * RigVMTypeUtils::GetWildCardCPPTypeObject()

static UObject * RigVMTypeUtils::ObjectFromCPPType ( FString& InOutCPPType, bool bUseRedirector, const FRigVMUserDefinedTypeResolver* InTypeResolver )

static FString RigVMTypeUtils::PostProcessCPPType ( const FString& InCPPType, UObject* InCPPTypeObject, const FRigVMUserDefinedTypeResolver* InResolvalInfo )

static bool RigVMTypeUtils::RequiresCPPTypeObject ( const FString& InCPPType )



---

## RivermaxCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RivermaxCore

**Contents:**
- RivermaxCore
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

const TCHAR * UE::RivermaxCore::LexToString ( ESamplingType InType )

const TCHAR * UE::RivermaxCore::LexToString ( ERivermaxAlignmentMode InValue )

const TCHAR * UE::RivermaxCore::LexToString ( EFrameLockingMode InValue )



---

## RivermaxEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RivermaxEditor

**Contents:**
- RivermaxEditor
- Navigation



---

## RivermaxMedia

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RivermaxMedia

**Contents:**
- RivermaxMedia
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## RivermaxRendering

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RivermaxRendering

**Contents:**
- RivermaxRendering
- Navigation
- Classes



---

## RivermaxSync

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RivermaxSync

**Contents:**
- RivermaxSync
- Navigation
- Classes
- Structs



---

## RuntimeTelemetry

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RuntimeTelemetry

**Contents:**
- RuntimeTelemetry
- Navigation
- Classes



---

## RuntimeTests

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/RuntimeTests

**Contents:**
- RuntimeTests
- Navigation
- Classes
- Structs



---

## SampleToolsEditorMode

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SampleToolsEditorMode

**Contents:**
- SampleToolsEditorMode
- Navigation
- Classes



---

## SceneStateBinding

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SceneStateBinding

**Contents:**
- SceneStateBinding
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

const FLazyName UE::SceneState::Metadata::CanRefToArray ( TEXT("CanRefToArray") )

const FLazyName UE::SceneState::Metadata::IsRefToArray ( TEXT("IsRefToArray") )

const FLazyName UE::SceneState::Metadata::NoBindingContainerSelfOnly ( TEXT("NoBindingContainerSelfOnly") )

const FLazyName UE::SceneState::Metadata::NoBindingSelfOnly ( TEXT("NoBindingSelfOnly") )

const FLazyName UE::SceneState::Metadata::RefType ( TEXT("RefType") )



---

## SceneStateBlueprintEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SceneStateBlueprintEditor

**Contents:**
- SceneStateBlueprintEditor
- Navigation
- Classes
- Interfaces



---

## SceneStateBlueprint

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SceneStateBlueprint

**Contents:**
- SceneStateBlueprint
- Navigation
- Classes
- Structs



---

## SceneStateDataLink

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SceneStateDataLink

**Contents:**
- SceneStateDataLink
- Navigation
- Structs



---

## SceneStateEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SceneStateEditor

**Contents:**
- SceneStateEditor
- Navigation
- Classes
- Structs



---

## SceneStateEvent

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SceneStateEvent

**Contents:**
- SceneStateEvent
- Navigation
- Classes
- Structs
- Interfaces



---

## SceneStateGameplay

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SceneStateGameplay

**Contents:**
- SceneStateGameplay
- Navigation
- Classes



---

## SceneStateTasks

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SceneStateTasks

**Contents:**
- SceneStateTasks
- Navigation
- Structs



---

## SceneStateTransitionGraph

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SceneStateTransitionGraph

**Contents:**
- SceneStateTransitionGraph
- Navigation
- Classes
- Interfaces



---

## SceneState

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SceneState

**Contents:**
- SceneState
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

ENUM_CLASS_FLAGS ( ESceneStateTaskFlags )

ENUM_CLASS_FLAGS ( ESceneStateTransitionEvaluationFlags )



---

## ScreenReader

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ScreenReader

**Contents:**
- ScreenReader
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## ScriptableToolsEditorMode

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ScriptableToolsEditorMode

**Contents:**
- ScriptableToolsEditorMode
- Navigation
- Classes



---

## ScriptableToolsFramework

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ScriptableToolsFramework

**Contents:**
- ScriptableToolsFramework
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

bool operator! ( EScriptableToolGizmoTranslation E )

bool operator! ( EScriptableToolGizmoRotation E )

bool operator! ( EScriptableToolGizmoScale E )

EScriptableToolGizmoTranslation operator& ( EScriptableToolGizmoTranslation Lhs, EScriptableToolGizmoTranslation Rhs )

EScriptableToolGizmoRotation operator& ( EScriptableToolGizmoRotation Lhs, EScriptableToolGizmoRotation Rhs )

EScriptableToolGizmoScale operator& ( EScriptableToolGizmoScale Lhs, EScriptableToolGizmoScale Rhs )

EScriptableToolGizmoTranslation & operator&= ( EScriptableToolGizmoTranslation& Lhs, EScriptableToolGizmoTranslation Rhs )

EScriptableToolGizmoRotation & operator&= ( EScriptableToolGizmoRotation& Lhs, EScriptableToolGizmoRotation Rhs )

EScriptableToolGizmoScale & operator&= ( EScriptableToolGizmoScale& Lhs, EScriptableToolGizmoScale Rhs )

EScriptableToolGizmoTranslation operator^ ( EScriptableToolGizmoTranslation Lhs, EScriptableToolGizmoTranslation Rhs )

EScriptableToolGizmoRotation operator^ ( EScriptableToolGizmoRotation Lhs, EScriptableToolGizmoRotation Rhs )

EScriptableToolGizmoScale operator^ ( EScriptableToolGizmoScale Lhs, EScriptableToolGizmoScale Rhs )

EScriptableToolGizmoTranslation & operator^= ( EScriptableToolGizmoTranslation& Lhs, EScriptableToolGizmoTranslation Rhs )

EScriptableToolGizmoRotation & operator^= ( EScriptableToolGizmoRotation& Lhs, EScriptableToolGizmoRotation Rhs )

EScriptableToolGizmoScale & operator^= ( EScriptableToolGizmoScale& Lhs, EScriptableToolGizmoScale Rhs )

EScriptableToolGizmoTranslation operator| ( EScriptableToolGizmoTranslation Lhs, EScriptableToolGizmoTranslation Rhs )

EScriptableToolGizmoRotation operator| ( EScriptableToolGizmoRotation Lhs, EScriptableToolGizmoRotation Rhs )

EScriptableToolGizmoScale operator| ( EScriptableToolGizmoScale Lhs, EScriptableToolGizmoScale Rhs )

EScriptableToolGizmoTranslation & operator|= ( EScriptableToolGizmoTranslation& Lhs, EScriptableToolGizmoTranslation Rhs )

EScriptableToolGizmoRotation & operator|= ( EScriptableToolGizmoRotation& Lhs, EScriptableToolGizmoRotation Rhs )

EScriptableToolGizmoScale & operator|= ( EScriptableToolGizmoScale& Lhs, EScriptableToolGizmoScale Rhs )

EScriptableToolGizmoTranslation operator~ ( EScriptableToolGizmoTranslation E )

EScriptableToolGizmoRotation operator~ ( EScriptableToolGizmoRotation E )

EScriptableToolGizmoScale operator~ ( EScriptableToolGizmoScale E )



---

## ScriptEditorPlugin

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ScriptEditorPlugin

**Contents:**
- ScriptEditorPlugin
- Navigation
- Classes
- Interfaces



---

## ScriptPlugin

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ScriptPlugin

**Contents:**
- ScriptPlugin
- Navigation
- Classes
- Structs
- Interfaces



---

## SecuritySandbox

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SecuritySandbox

**Contents:**
- SecuritySandbox
- Navigation
- Classes
- Interfaces



---

## SequenceNavigator

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SequenceNavigator

**Contents:**
- SequenceNavigator
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

ENUM_CLASS_FLAGS ( ENavigationToolItemViewMode )

bool operator! ( ENavigationToolFilterMode E )

bool operator! ( ENavigationToolItemSelectionFlags E )

bool operator! ( ENavigationToolIgnoreNotifyFlags E )

ENavigationToolFilterMode operator& ( ENavigationToolFilterMode Lhs, ENavigationToolFilterMode Rhs )

ENavigationToolItemSelectionFlags operator& ( ENavigationToolItemSelectionFlags Lhs, ENavigationToolItemSelectionFlags Rhs )

ENavigationToolIgnoreNotifyFlags operator& ( ENavigationToolIgnoreNotifyFlags Lhs, ENavigationToolIgnoreNotifyFlags Rhs )

ENavigationToolFilterMode & operator&= ( ENavigationToolFilterMode& Lhs, ENavigationToolFilterMode Rhs )

ENavigationToolItemSelectionFlags & operator&= ( ENavigationToolItemSelectionFlags& Lhs, ENavigationToolItemSelectionFlags Rhs )

ENavigationToolIgnoreNotifyFlags & operator&= ( ENavigationToolIgnoreNotifyFlags& Lhs, ENavigationToolIgnoreNotifyFlags Rhs )

ENavigationToolFilterMode operator^ ( ENavigationToolFilterMode Lhs, ENavigationToolFilterMode Rhs )

ENavigationToolItemSelectionFlags operator^ ( ENavigationToolItemSelectionFlags Lhs, ENavigationToolItemSelectionFlags Rhs )

ENavigationToolIgnoreNotifyFlags operator^ ( ENavigationToolIgnoreNotifyFlags Lhs, ENavigationToolIgnoreNotifyFlags Rhs )

ENavigationToolFilterMode & operator^= ( ENavigationToolFilterMode& Lhs, ENavigationToolFilterMode Rhs )

ENavigationToolItemSelectionFlags & operator^= ( ENavigationToolItemSelectionFlags& Lhs, ENavigationToolItemSelectionFlags Rhs )

ENavigationToolIgnoreNotifyFlags & operator^= ( ENavigationToolIgnoreNotifyFlags& Lhs, ENavigationToolIgnoreNotifyFlags Rhs )

ENavigationToolFilterMode operator| ( ENavigationToolFilterMode Lhs, ENavigationToolFilterMode Rhs )

ENavigationToolItemSelectionFlags operator| ( ENavigationToolItemSelectionFlags Lhs, ENavigationToolItemSelectionFlags Rhs )

ENavigationToolIgnoreNotifyFlags operator| ( ENavigationToolIgnoreNotifyFlags Lhs, ENavigationToolIgnoreNotifyFlags Rhs )

ENavigationToolFilterMode & operator|= ( ENavigationToolFilterMode& Lhs, ENavigationToolFilterMode Rhs )

ENavigationToolItemSelectionFlags & operator|= ( ENavigationToolItemSelectionFlags& Lhs, ENavigationToolItemSelectionFlags Rhs )

ENavigationToolIgnoreNotifyFlags & operator|= ( ENavigationToolIgnoreNotifyFlags& Lhs, ENavigationToolIgnoreNotifyFlags Rhs )

ENavigationToolFilterMode operator~ ( ENavigationToolFilterMode E )

ENavigationToolItemSelectionFlags operator~ ( ENavigationToolItemSelectionFlags E )

ENavigationToolIgnoreNotifyFlags operator~ ( ENavigationToolIgnoreNotifyFlags E )

ENavigationToolCompareState UE::SequenceNavigator::ItemUtils::CompareArrayState ( const TArray< InItemType* >& InArray, const TFunctionRef< bool(const InItemType*const)>& InTrueFunction, const TFunctionRef< bool(const InItemType*const)>& InFalseFunction )

ENavigationToolCompareState UE::SequenceNavigator::ItemUtils::CompareArrayStateSimple ( const TArray< InItemType* >& InArray, const TFunctionRef< bool(const InItemType*const)>& InTrueFunction )

ENavigationToolCompareState UE::SequenceNavigator::ItemUtils::CompareChildrenItemState ( const FNavigationToolViewModelPtr& InItem, const TFunctionRef< bool(const Sequencer::TViewModelPtr< InItemType >)>& InTrueFunction, const TFunctionRef< bool(const Sequencer::TViewModelPtr< InItemType >)>& InFalseFunction, const ENavigationToolCompareState InDefaultState )

ENavigationToolCompareState UE::SequenceNavigator::ItemUtils::CompareChildrenItemStateSimple ( const FNavigationToolViewModelPtr& InItem, const TFunctionRef< bool(const InItemType*const)>& InTrueFunction )

bool UE::SequenceNavigator::ItemUtils::operator! ( ENavigationToolCompareState E )

ENavigationToolCompareState UE::SequenceNavigator::ItemUtils::operator& ( ENavigationToolCompareState Lhs, ENavigationToolCompareState Rhs )

ENavigationToolCompareState & UE::SequenceNavigator::ItemUtils::operator&= ( ENavigationToolCompareState& Lhs, ENavigationToolCompareState Rhs )

ENavigationToolCompareState UE::SequenceNavigator::ItemUtils::operator^ ( ENavigationToolCompareState Lhs, ENavigationToolCompareState Rhs )

ENavigationToolCompareState & UE::SequenceNavigator::ItemUtils::operator^= ( ENavigationToolCompareState& Lhs, ENavigationToolCompareState Rhs )

ENavigationToolCompareState UE::SequenceNavigator::ItemUtils::operator| ( ENavigationToolCompareState Lhs, ENavigationToolCompareState Rhs )

ENavigationToolCompareState & UE::SequenceNavigator::ItemUtils::operator|= ( ENavigationToolCompareState& Lhs, ENavigationToolCompareState Rhs )

ENavigationToolCompareState UE::SequenceNavigator::ItemUtils::operator~ ( ENavigationToolCompareState E )

bool UE::SequenceNavigator::operator! ( EItemMarkerVisibility E )

bool UE::SequenceNavigator::operator! ( EItemContainsPlayhead E )

bool UE::SequenceNavigator::operator! ( EItemRevisionControlState E )

bool UE::SequenceNavigator::operator! ( ENavigationToolAddItemFlags E )

EItemMarkerVisibility UE::SequenceNavigator::operator& ( EItemMarkerVisibility Lhs, EItemMarkerVisibility Rhs )

EItemContainsPlayhead UE::SequenceNavigator::operator& ( EItemContainsPlayhead Lhs, EItemContainsPlayhead Rhs )

EItemRevisionControlState UE::SequenceNavigator::operator& ( EItemRevisionControlState Lhs, EItemRevisionControlState Rhs )

ENavigationToolAddItemFlags UE::SequenceNavigator::operator& ( ENavigationToolAddItemFlags Lhs, ENavigationToolAddItemFlags Rhs )

EItemMarkerVisibility & UE::SequenceNavigator::operator&= ( EItemMarkerVisibility& Lhs, EItemMarkerVisibility Rhs )

EItemContainsPlayhead & UE::SequenceNavigator::operator&= ( EItemContainsPlayhead& Lhs, EItemContainsPlayhead Rhs )

EItemRevisionControlState & UE::SequenceNavigator::operator&= ( EItemRevisionControlState& Lhs, EItemRevisionControlState Rhs )

ENavigationToolAddItemFlags & UE::SequenceNavigator::operator&= ( ENavigationToolAddItemFlags& Lhs, ENavigationToolAddItemFlags Rhs )

EItemMarkerVisibility UE::SequenceNavigator::operator^ ( EItemMarkerVisibility Lhs, EItemMarkerVisibility Rhs )

EItemContainsPlayhead UE::SequenceNavigator::operator^ ( EItemContainsPlayhead Lhs, EItemContainsPlayhead Rhs )

EItemRevisionControlState UE::SequenceNavigator::operator^ ( EItemRevisionControlState Lhs, EItemRevisionControlState Rhs )

ENavigationToolAddItemFlags UE::SequenceNavigator::operator^ ( ENavigationToolAddItemFlags Lhs, ENavigationToolAddItemFlags Rhs )

EItemMarkerVisibility & UE::SequenceNavigator::operator^= ( EItemMarkerVisibility& Lhs, EItemMarkerVisibility Rhs )

EItemContainsPlayhead & UE::SequenceNavigator::operator^= ( EItemContainsPlayhead& Lhs, EItemContainsPlayhead Rhs )

EItemRevisionControlState & UE::SequenceNavigator::operator^= ( EItemRevisionControlState& Lhs, EItemRevisionControlState Rhs )

ENavigationToolAddItemFlags & UE::SequenceNavigator::operator^= ( ENavigationToolAddItemFlags& Lhs, ENavigationToolAddItemFlags Rhs )

EItemMarkerVisibility UE::SequenceNavigator::operator| ( EItemMarkerVisibility Lhs, EItemMarkerVisibility Rhs )

EItemContainsPlayhead UE::SequenceNavigator::operator| ( EItemContainsPlayhead Lhs, EItemContainsPlayhead Rhs )

EItemRevisionControlState UE::SequenceNavigator::operator| ( EItemRevisionControlState Lhs, EItemRevisionControlState Rhs )

ENavigationToolAddItemFlags UE::SequenceNavigator::operator| ( ENavigationToolAddItemFlags Lhs, ENavigationToolAddItemFlags Rhs )

EItemMarkerVisibility & UE::SequenceNavigator::operator|= ( EItemMarkerVisibility& Lhs, EItemMarkerVisibility Rhs )

EItemContainsPlayhead & UE::SequenceNavigator::operator|= ( EItemContainsPlayhead& Lhs, EItemContainsPlayhead Rhs )

EItemRevisionControlState & UE::SequenceNavigator::operator|= ( EItemRevisionControlState& Lhs, EItemRevisionControlState Rhs )

ENavigationToolAddItemFlags & UE::SequenceNavigator::operator|= ( ENavigationToolAddItemFlags& Lhs, ENavigationToolAddItemFlags Rhs )

EItemMarkerVisibility UE::SequenceNavigator::operator~ ( EItemMarkerVisibility E )

EItemContainsPlayhead UE::SequenceNavigator::operator~ ( EItemContainsPlayhead E )

EItemRevisionControlState UE::SequenceNavigator::operator~ ( EItemRevisionControlState E )

ENavigationToolAddItemFlags UE::SequenceNavigator::operator~ ( ENavigationToolAddItemFlags E )



---

## SequencerAnimTools

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SequencerAnimTools

**Contents:**
- SequencerAnimTools
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## SequencerPlaylists

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SequencerPlaylists

**Contents:**
- SequencerPlaylists
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## SequencerScriptingEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SequencerScriptingEditor

**Contents:**
- SequencerScriptingEditor
- Navigation
- Classes
- Structs



---

## SequencerScripting

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SequencerScripting

**Contents:**
- SequencerScripting
- Navigation
- Classes
- Structs



---

## SequenceValidator

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SequenceValidator

**Contents:**
- SequenceValidator
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## Shaders in Plugins

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/shaders-in-plugins-for-unreal-engine

**Contents:**
- Shaders in Plugins
- Topic List

Information on creating and using shaders in plugins.

The following documents will go over all of the various items that you need to be aware of when trying to create and use global shaders via a Plugin.



---

## SharedMemoryMedia

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SharedMemoryMedia

**Contents:**
- SharedMemoryMedia
- Navigation
- Classes
- Enums
  - Public
- Variables
  - Public



---

## Shotgrid

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Shotgrid

**Contents:**
- Shotgrid
- Navigation
- Interfaces



---

## SignificanceManager

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SignificanceManager

**Contents:**
- SignificanceManager
- Navigation
- Classes
- Structs
- Variables
  - Public



---

## SimpleHMD

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SimpleHMD

**Contents:**
- SimpleHMD
- Navigation
- Interfaces



---

## SkeletalMerging

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SkeletalMerging

**Contents:**
- SkeletalMerging
- Navigation
- Classes
- Structs



---

## SkeletalMeshModelingTools

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SkeletalMeshModelingTools

**Contents:**
- SkeletalMeshModelingTools
- Navigation
- Interfaces



---

## SkeletalMeshModifiers

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SkeletalMeshModifiers

**Contents:**
- SkeletalMeshModifiers
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

bool operator! ( ESkeletalMeshModificationType E )

bool operator! ( ESkeletonModificationType E )

ESkeletalMeshModificationType operator& ( ESkeletalMeshModificationType Lhs, ESkeletalMeshModificationType Rhs )

ESkeletonModificationType operator& ( ESkeletonModificationType Lhs, ESkeletonModificationType Rhs )

ESkeletalMeshModificationType & operator&= ( ESkeletalMeshModificationType& Lhs, ESkeletalMeshModificationType Rhs )

ESkeletonModificationType & operator&= ( ESkeletonModificationType& Lhs, ESkeletonModificationType Rhs )

ESkeletalMeshModificationType operator^ ( ESkeletalMeshModificationType Lhs, ESkeletalMeshModificationType Rhs )

ESkeletonModificationType operator^ ( ESkeletonModificationType Lhs, ESkeletonModificationType Rhs )

ESkeletalMeshModificationType & operator^= ( ESkeletalMeshModificationType& Lhs, ESkeletalMeshModificationType Rhs )

ESkeletonModificationType & operator^= ( ESkeletonModificationType& Lhs, ESkeletonModificationType Rhs )

ESkeletalMeshModificationType operator| ( ESkeletalMeshModificationType Lhs, ESkeletalMeshModificationType Rhs )

ESkeletonModificationType operator| ( ESkeletonModificationType Lhs, ESkeletonModificationType Rhs )

ESkeletalMeshModificationType & operator|= ( ESkeletalMeshModificationType& Lhs, ESkeletalMeshModificationType Rhs )

ESkeletonModificationType & operator|= ( ESkeletonModificationType& Lhs, ESkeletonModificationType Rhs )

ESkeletalMeshModificationType operator~ ( ESkeletalMeshModificationType E )

ESkeletonModificationType operator~ ( ESkeletonModificationType E )



---

## SkeletalMeshMorphTargetEditingTools

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SkeletalMeshMorphTargetEditingTo-

**Contents:**
- SkeletalMeshMorphTargetEditingTools
- Navigation
- Classes
- Interfaces



---

## SkeletalMeshReduction

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SkeletalMeshReduction

**Contents:**
- SkeletalMeshReduction
- Navigation
- Interfaces



---

## SlateIMInGame

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SlateIMInGame

**Contents:**
- SlateIMInGame
- Navigation
- Classes
- Variables
  - Public



---

## SlateIM

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SlateIM

**Contents:**
- SlateIM
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

bool SlateIM::BeginViewportRoot ( FName UniqueName, TSharedPtr< IAssetViewport > AssetViewport, const FViewportRootLayout& Layout )



---

## SlateMVVM

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SlateMVVM

**Contents:**
- SlateMVVM
- Navigation
- Classes
- Structs



---

## SlateScreenReader

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SlateScreenReader

**Contents:**
- SlateScreenReader
- Navigation
- Classes
- Interfaces



---

## SlateScriptingCommands

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SlateScriptingCommands

**Contents:**
- SlateScriptingCommands
- Navigation
- Classes
- Structs



---

## SmartObjectsEditorModule

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SmartObjectsEditorModule

**Contents:**
- SmartObjectsEditorModule
- Navigation
- Classes
- Interfaces



---

## SmartObjectsModule

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SmartObjectsModule

**Contents:**
- SmartObjectsModule
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## SmartObjectsTestSuite

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SmartObjectsTestSuite

**Contents:**
- SmartObjectsTestSuite
- Navigation
- Classes
- Structs
- Interfaces



---

## SocketSubsystemEOS

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SocketSubsystemEOS

**Contents:**
- SocketSubsystemEOS
- Navigation
- Classes
- Interfaces
- Typedefs



---

## SocketSubsystemSteamIP

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SocketSubsystemSteamIP

**Contents:**
- SocketSubsystemSteamIP
- Navigation
- Classes
- Variables
  - Public
- Functions
  - Public

FName CreateSteamSocketSubsystem()

void DestroySteamSocketSubsystem()



---

## SoundCueTemplatesEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SoundCueTemplatesEditor

**Contents:**
- SoundCueTemplatesEditor
- Navigation
- Classes



---

## SoundCueTemplates

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SoundCueTemplates

**Contents:**
- SoundCueTemplates
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## SoundFields

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SoundFields

**Contents:**
- SoundFields
- Navigation
- Classes



---

## SoundModImporter

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SoundModImporter

**Contents:**
- SoundModImporter
- Navigation
- Classes



---

## SoundMod

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SoundMod

**Contents:**
- SoundMod
- Navigation
- Classes
- Interfaces



---

## SoundScapeEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SoundScapeEditor

**Contents:**
- SoundScapeEditor
- Navigation
- Classes



---

## SoundScape

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SoundScape

**Contents:**
- SoundScape
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## SoundUtilitiesEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SoundUtilitiesEditor

**Contents:**
- SoundUtilitiesEditor
- Navigation
- Classes



---

## SoundUtilities

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SoundUtilities

**Contents:**
- SoundUtilities
- Navigation
- Classes
- Structs



---

## SourceFilteringCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SourceFilteringCore

**Contents:**
- SourceFilteringCore
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

ENUM_RANGE_BY_COUNT ( EFilterSetMode, EFilterSetMode::Count )



---

## SourceFilteringTrace

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SourceFilteringTrace

**Contents:**
- SourceFilteringTrace
- Navigation
- Classes
- Structs



---

## SpatializationEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SpatializationEditor

**Contents:**
- SpatializationEditor
- Navigation
- Classes



---

## Spatialization

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Spatialization

**Contents:**
- Spatialization
- Navigation
- Classes
- Structs



---

## SpatialReadiness

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SpatialReadiness

**Contents:**
- SpatialReadiness
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## SpeedTreeImporter

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SpeedTreeImporter

**Contents:**
- SpeedTreeImporter
- Navigation
- Classes
- Interfaces
- Enums
  - Public



---

## SQLiteCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SQLiteCore

**Contents:**
- SQLiteCore
- Navigation
- Classes
- Structs
- Enums
  - Public
- Functions
  - Public

bool operator! ( ESQLitePreparedStatementFlags E )

ESQLitePreparedStatementFlags operator& ( ESQLitePreparedStatementFlags Lhs, ESQLitePreparedStatementFlags Rhs )

ESQLitePreparedStatementFlags & operator&= ( ESQLitePreparedStatementFlags& Lhs, ESQLitePreparedStatementFlags Rhs )

ESQLitePreparedStatementFlags operator^ ( ESQLitePreparedStatementFlags Lhs, ESQLitePreparedStatementFlags Rhs )

ESQLitePreparedStatementFlags & operator^= ( ESQLitePreparedStatementFlags& Lhs, ESQLitePreparedStatementFlags Rhs )

ESQLitePreparedStatementFlags operator| ( ESQLitePreparedStatementFlags Lhs, ESQLitePreparedStatementFlags Rhs )

ESQLitePreparedStatementFlags & operator|= ( ESQLitePreparedStatementFlags& Lhs, ESQLitePreparedStatementFlags Rhs )

ESQLitePreparedStatementFlags operator~ ( ESQLitePreparedStatementFlags E )



---

## SQLiteSupport

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SQLiteSupport

**Contents:**
- SQLiteSupport
- Navigation
- Classes
- Interfaces



---

## StageDataProvider

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StageDataProvider

**Contents:**
- StageDataProvider
- Navigation
- Interfaces



---

## StageMonitorCommon

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StageMonitorCommon

**Contents:**
- StageMonitorCommon
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## StageMonitor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StageMonitor

**Contents:**
- StageMonitor
- Navigation
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

bool operator! ( EGetProviderFlags E )

EGetProviderFlags operator& ( EGetProviderFlags Lhs, EGetProviderFlags Rhs )

EGetProviderFlags & operator&= ( EGetProviderFlags& Lhs, EGetProviderFlags Rhs )

EGetProviderFlags operator^ ( EGetProviderFlags Lhs, EGetProviderFlags Rhs )

EGetProviderFlags & operator^= ( EGetProviderFlags& Lhs, EGetProviderFlags Rhs )

EGetProviderFlags operator| ( EGetProviderFlags Lhs, EGetProviderFlags Rhs )

EGetProviderFlags & operator|= ( EGetProviderFlags& Lhs, EGetProviderFlags Rhs )

EGetProviderFlags operator~ ( EGetProviderFlags E )



---

## StallLogSubsystem

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StallLogSubsystem

**Contents:**
- StallLogSubsystem
- Navigation
- Classes



---

## StateGraphManager

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StateGraphManager

**Contents:**
- StateGraphManager
- Navigation
- Classes



---

## StateGraph

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StateGraph

**Contents:**
- StateGraph
- Navigation
- Classes
- Typedefs



---

## StateTreeDeveloper

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StateTreeDeveloper

**Contents:**
- StateTreeDeveloper
- Navigation
- Classes



---

## StateTreeEditorModule

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StateTreeEditorModule

**Contents:**
- StateTreeEditorModule
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Variables
  - Public



---

## StateTreeModule

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StateTreeModule

**Contents:**
- StateTreeModule
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Constants
- Variables

Type of the copy | StateTreePropertyBindings.h | |

FStateTreePropertyPath ( const FPropertyBindingPath& Other )

FStateTreeStrongTaskRef ( TStrongObjectPtr< const UStateTree > StateTree, const FStateTreeTaskBase* Task, FStateTreeIndex16 NodeIndex, FGuid NodeId )

const UStateTree * GetStateTree()

const FStateTreeTaskBase * GetTask()

FStateTreeIndex16 GetTaskIndex()

bool operator! ( EStateTreeStateSelectionRules E )

bool operator! ( EStateTreeTransitionTrigger E )

bool operator!= ( const EStateTreeTransitionPriority Lhs, const EStateTreeTransitionPriority Rhs )

EStateTreeStateSelectionRules operator& ( EStateTreeStateSelectionRules Lhs, EStateTreeStateSelectionRules Rhs )

EStateTreeTransitionTrigger operator& ( EStateTreeTransitionTrigger Lhs, EStateTreeTransitionTrigger Rhs )

EStateTreeStateSelectionRules & operator&= ( EStateTreeStateSelectionRules& Lhs, EStateTreeStateSelectionRules Rhs )

EStateTreeTransitionTrigger & operator&= ( EStateTreeTransitionTrigger& Lhs, EStateTreeTransitionTrigger Rhs )

EStateTreeStateSelectionRules operator^ ( EStateTreeStateSelectionRules Lhs, EStateTreeStateSelectionRules Rhs )

EStateTreeTransitionTrigger operator^ ( EStateTreeTransitionTrigger Lhs, EStateTreeTransitionTrigger Rhs )

EStateTreeStateSelectionRules & operator^= ( EStateTreeStateSelectionRules& Lhs, EStateTreeStateSelectionRules Rhs )

EStateTreeTransitionTrigger & operator^= ( EStateTreeTransitionTrigger& Lhs, EStateTreeTransitionTrigger Rhs )

EStateTreeStateSelectionRules operator| ( EStateTreeStateSelectionRules Lhs, EStateTreeStateSelectionRules Rhs )

EStateTreeTransitionTrigger operator| ( EStateTreeTransitionTrigger Lhs, EStateTreeTransitionTrigger Rhs )

EStateTreeStateSelectionRules & operator|= ( EStateTreeStateSelectionRules& Lhs, EStateTreeStateSelectionRules Rhs )

EStateTreeTransitionTrigger & operator|= ( EStateTreeTransitionTrigger& Lhs, EStateTreeTransitionTrigger Rhs )

EStateTreeStateSelectionRules operator~ ( EStateTreeStateSelectionRules E )

EStateTreeTransitionTrigger operator~ ( EStateTreeTransitionTrigger E )

bool operator== ( const EStateTreeTransitionPriority Lhs, const EStateTreeTransitionPriority Rhs )

bool operator> ( const EStateTreeTransitionPriority Lhs, const EStateTreeTransitionPriority Rhs )

bool operator>= ( const EStateTreeTransitionPriority Lhs, const EStateTreeTransitionPriority Rhs )

UE::StateTree::Debug::DECLARE_TS_MULTICAST_DELEGATE_ThreeParams ( FPhaseDelegate, const FStateTreeExecutionContext&, EStateTreeUpdatePhase, FStateTreeStateHandle )

UE::StateTree::Debug::DECLARE_TS_MULTICAST_DELEGATE_ThreeParams ( FStateDelegate, const FStateTreeExecutionContext&, FStateTreeStateHandle, EStateTreeTraceEventType )

UE::StateTree::Debug::DECLARE_TS_MULTICAST_DELEGATE_ThreeParams ( FTransitionDelegate, const FStateTreeExecutionContext&, const FStateTreeTransitionSource&, EStateTreeTraceEventType )

UE::StateTree::Debug::DECLARE_TS_MULTICAST_DELEGATE_TwoParams ( FEventSentDelegate, const FStateTreeMinimalExecutionContext& ExecutionContext, const FEventSentDelegateArgs& EventSentArgs )

UE::StateTree::Debug::DECLARE_TS_MULTICAST_DELEGATE_TwoParams ( FEventConsumedDelegate, const FStateTreeExecutionContext& ExecutionContext, const FStateTreeSharedEvent& Event )

UE::StateTree::Debug::DECLARE_TS_MULTICAST_DELEGATE_TwoParams ( FNodeDelegate, const FStateTreeExecutionContext&, FNodeDelegateArgs )

FText UE::StateTree::DescHelpers::GetDescriptionForMathOperation ( FText OperationText, const FGuid& ID, FStateTreeDataView InstanceDataView, const IStateTreeBindingLookup& BindingLookup, EStateTreeNodeFormatting Formatting )

FText UE::StateTree::DescHelpers::GetDescriptionForSingleParameterFunc ( FText OperationText, const FGuid& ID, FStateTreeDataView InstanceDataView, const IStateTreeBindingLookup& BindingLookup, EStateTreeNodeFormatting Formatting )

bool UE::StateTree::PropertyRefHelpers::IsPropertyCompatibleWithClass ( const FProperty& Property, const UClass& Class )

bool UE::StateTree::PropertyRefHelpers::IsPropertyCompatibleWithEnum ( const FProperty& Property, const UEnum& Enum )

bool UE::StateTree::PropertyRefHelpers::IsPropertyCompatibleWithStruct ( const FProperty& Property, const UScriptStruct& Struct )

const FName UE::StateTree::SchemaCanBeOverridenTag ( TEXT("SchemaCanBeOverriden") )

const FName UE::StateTree::SchemaTag ( TEXT("Schema") )

static EStateTreeDataSourceType UE::StateTree::CastToDataSourceType ( EStateTreeParameterDataType Value )

static T * UE::StateTree::PropertyRefHelpers::GetMutablePtrToProperty ( const FStateTreePropertyRef& PropertyRef, FStateTreeInstanceStorage& InstanceDataStorage, const FStateTreeExecutionFrame& ExecutionFrame, const FStateTreeExecutionFrame* ParentExecutionFrame, const FProperty** OutSourceProperty )

static TTuple< T *... > UE::StateTree::PropertyRefHelpers::GetMutablePtrTupleToProperty ( const FStateTreePropertyRef& PropertyRef, FStateTreeInstanceStorage& InstanceDataStorage, const FStateTreeExecutionFrame& ExecutionFrame, const FStateTreeExecutionFrame* ParentExecutionFrame )



---

## StateTreeTestSuite

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StateTreeTestSuite

**Contents:**
- StateTreeTestSuite
- Navigation
- Structs
- Interfaces



---

## StaticMeshEditorModeling

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StaticMeshEditorModeling

**Contents:**
- StaticMeshEditorModeling
- Navigation
- Classes



---

## SteamAudio

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SteamAudio

**Contents:**
- SteamAudio
- Navigation
- Interfaces



---

## SteamController

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SteamController

**Contents:**
- SteamController
- Navigation
- Interfaces



---

## SteamShared

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SteamShared

**Contents:**
- SteamShared
- Navigation
- Classes
- Interfaces
- Variables
  - Public



---

## SteamSockets

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SteamSockets

**Contents:**
- SteamSockets
- Navigation
- Classes
- Typedefs



---

## StereoCameraMetadata

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StereoCameraMetadata

**Contents:**
- StereoCameraMetadata
- Navigation



---

## StormSyncAvaBridge

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StormSyncAvaBridge

**Contents:**
- StormSyncAvaBridge
- Navigation
- Classes
- Constants



---

## StormSyncCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StormSyncCore

**Contents:**
- StormSyncCore
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public



---

## StormSyncDrives

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StormSyncDrives

**Contents:**
- StormSyncDrives
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public



---

## StormSyncEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StormSyncEditor

**Contents:**
- StormSyncEditor
- Navigation
- Classes
- Structs
- Interfaces



---

## StormSyncTransportClient

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StormSyncTransportClient

**Contents:**
- StormSyncTransportClient
- Navigation
- Interfaces
- Typedefs



---

## StormSyncTransportCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StormSyncTransportCore

**Contents:**
- StormSyncTransportCore
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Constants
- Functions
  - Public

bool UE::StormSync::Transport::Private::GetServerEndpointParam ( FString& OutEndpointValue, const FString& InDefaultHostName )

bool UE::StormSync::Transport::Private::IsServerAutoStartDisabled()



---

## StormSyncTransportServer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StormSyncTransportServer

**Contents:**
- StormSyncTransportServer
- Navigation
- Interfaces



---

## StructUtilsEngine

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StructUtilsEngine

**Contents:**
- StructUtilsEngine
- Navigation



---

## StructUtils

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StructUtils

**Contents:**
- StructUtils
- Navigation



---

## StylusInput

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/StylusInput

**Contents:**
- StylusInput
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

EPenStatus UE::StylusInput::operator& ( EPenStatus A, EPenStatus B )

ETabletHardwareCapabilities UE::StylusInput::operator& ( ETabletHardwareCapabilities A, ETabletHardwareCapabilities B )

ETabletSupportedProperties UE::StylusInput::operator& ( ETabletSupportedProperties A, ETabletSupportedProperties B )

EPenStatus UE::StylusInput::operator^ ( EPenStatus A, EPenStatus B )

ETabletHardwareCapabilities UE::StylusInput::operator^ ( ETabletHardwareCapabilities A, ETabletHardwareCapabilities B )

ETabletSupportedProperties UE::StylusInput::operator^ ( ETabletSupportedProperties A, ETabletSupportedProperties B )

EPenStatus UE::StylusInput::operator| ( EPenStatus A, EPenStatus B )

ETabletHardwareCapabilities UE::StylusInput::operator| ( ETabletHardwareCapabilities A, ETabletHardwareCapabilities B )

ETabletSupportedProperties UE::StylusInput::operator| ( ETabletSupportedProperties A, ETabletSupportedProperties B )

EPenStatus UE::StylusInput::operator~ ( EPenStatus A )

ETabletHardwareCapabilities UE::StylusInput::operator~ ( ETabletHardwareCapabilities A )

ETabletSupportedProperties UE::StylusInput::operator~ ( ETabletSupportedProperties A )

void UE::StylusInput::Private::Log ( const FString& Preamble, const FString& Message )

void UE::StylusInput::Private::LogError ( const FString& Preamble, const FString& Message )

void UE::StylusInput::Private::LogVerbose ( const FString& Preamble, const FString& Message )

void UE::StylusInput::Private::LogWarning ( const FString& Preamble, const FString& Message )



---

## SubtitlesAndClosedCaptionsEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SubtitlesAndClosedCaptionsEditor

**Contents:**
- SubtitlesAndClosedCaptionsEditor
- Navigation
- Classes
- Interfaces



---

## SubtitlesAndClosedCaptions

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SubtitlesAndClosedCaptions

**Contents:**
- SubtitlesAndClosedCaptions
- Navigation
- Classes
- Structs



---

## SunPosition

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SunPosition

**Contents:**
- SunPosition
- Navigation
- Classes
- Structs



---

## SurfaceEffects

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SurfaceEffects

**Contents:**
- SurfaceEffects
- Navigation
- Classes
- Structs



---

## SVGImporterEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SVGImporterEditor

**Contents:**
- SVGImporterEditor
- Navigation
- Classes
- Interfaces



---

## SVGImporter

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SVGImporter

**Contents:**
- SVGImporter
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Constants



---

## SynthesisEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/SynthesisEditor

**Contents:**
- SynthesisEditor
- Navigation
- Classes



---

## Synthesis

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Synthesis

**Contents:**
- Synthesis
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## TakeMovieScene

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TakeMovieScene

**Contents:**
- TakeMovieScene
- Navigation
- Classes
- Structs



---

## TakeRecorderNamingTokens

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TakeRecorderNamingTokens

**Contents:**
- TakeRecorderNamingTokens
- Navigation
- Interfaces



---

## TakeRecorderSources

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TakeRecorderSources

**Contents:**
- TakeRecorderSources
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

void TakeRecorderSourceHelpers::ProcessRecordedTimes ( ULevelSequence* InSequence, UMovieSceneTakeTrack* TakeTrack, const TOptional< TRange< FFrameNumber > >& FrameRange, const FArrayOfRecordedTimePairs& RecordedTimes )



---

## TakeRecorder

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TakeRecorder

**Contents:**
- TakeRecorder
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

UE_TRACE_CHANNEL_EXTERN ( TakeRecorderChannel, TAKERECORDER_API )



---

## TakesCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TakesCore

**Contents:**
- TakesCore
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Functions
  - Public
  - Static

bool UE::TakesCore::operator! ( ETimecodeExtractionFlags E )

ETimecodeExtractionFlags UE::TakesCore::operator& ( ETimecodeExtractionFlags Lhs, ETimecodeExtractionFlags Rhs )

ETimecodeExtractionFlags & UE::TakesCore::operator&= ( ETimecodeExtractionFlags& Lhs, ETimecodeExtractionFlags Rhs )

ETimecodeExtractionFlags UE::TakesCore::operator^ ( ETimecodeExtractionFlags Lhs, ETimecodeExtractionFlags Rhs )

ETimecodeExtractionFlags & UE::TakesCore::operator^= ( ETimecodeExtractionFlags& Lhs, ETimecodeExtractionFlags Rhs )

ETimecodeExtractionFlags UE::TakesCore::operator| ( ETimecodeExtractionFlags Lhs, ETimecodeExtractionFlags Rhs )

ETimecodeExtractionFlags & UE::TakesCore::operator|= ( ETimecodeExtractionFlags& Lhs, ETimecodeExtractionFlags Rhs )

ETimecodeExtractionFlags UE::TakesCore::operator~ ( ETimecodeExtractionFlags E )

static bool TakesUtils::CreateNewAssetPackage ( FString& InPackageName, AssetType*& OutAsset, FText* OutError, AssetType* OptionalBase, UClass* OptionalClass )

static bool TakesUtils::CreateNewAssetPackage ( FString& InPackageName, TObjectPtr< AssetType >& OutAsset, FText* OutError, AssetType* OptionalBase, UClass* OptionalClass )

static AssetType * TakesUtils::MakeNewAsset ( const FString& BaseAssetPath, const FString& BaseAssetName )



---

## TakeSequencer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TakeSequencer

**Contents:**
- TakeSequencer
- Navigation
- Classes



---

## TakeTrackRecorders

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TakeTrackRecorders

**Contents:**
- TakeTrackRecorders
- Navigation
- Classes
- Structs
- Interfaces



---

## TargetDeviceServicesScripting

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TargetDeviceServicesScripting

**Contents:**
- TargetDeviceServicesScripting
- Navigation
- Classes
- Structs



---

## TargetingSystem

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TargetingSystem

**Contents:**
- TargetingSystem
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## TcpMessaging

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TcpMessaging

**Contents:**
- TcpMessaging
- Navigation
- Interfaces



---

## TechAudioToolsMetaSoundEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TechAudioToolsMetaSoundEditor

**Contents:**
- TechAudioToolsMetaSoundEditor
- Navigation
- Classes



---

## TechAudioToolsMetaSound

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TechAudioToolsMetaSound

**Contents:**
- TechAudioToolsMetaSound
- Navigation
- Classes
- Interfaces
- Functions
  - Public

FName TechAudioTools::MetaSound::GetAdjustedDataType ( const FName& DataType, const bool bIsArray )



---

## TechAudioTools

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TechAudioTools

**Contents:**
- TechAudioTools
- Navigation
- Classes
- Enums
  - Public
- Functions
  - Public

FFloatInterval TechAudioTools::ConvertRange ( UnitT FromUnits, UnitT ToUnits, FFloatInterval InputRange )

float TechAudioTools::ConvertUnit ( const ETechAudioToolsVolumeUnit FromUnits, const ETechAudioToolsVolumeUnit ToUnits, const float Value )

float TechAudioTools::ConvertUnit ( const ETechAudioToolsPitchUnit FromUnits, const ETechAudioToolsPitchUnit ToUnits, const float Value )



---

## TedsActorCompatibility

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TedsActorCompatibility

**Contents:**
- TedsActorCompatibility
- Navigation
- Structs



---

## TedsAlerts

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TedsAlerts

**Contents:**
- TedsAlerts
- Navigation
- Structs
- Typedefs
- Enums
  - Public



---

## TedsAssetData

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TedsAssetData

**Contents:**
- TedsAssetData
- Navigation
- Classes
- Structs
- Typedefs
- Constants



---

## TedsCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TedsCore

**Contents:**
- TedsCore
- Navigation
- Classes



---

## TedsEverythingPicker

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TedsEverythingPicker

**Contents:**
- TedsEverythingPicker
- Navigation
- Classes
- Typedefs



---

## TedsOutliner

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TedsOutliner

**Contents:**
- TedsOutliner
- Navigation
- Classes
- Structs
- Typedefs
- Constants



---

## TedsPropertyEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TedsPropertyEditor

**Contents:**
- TedsPropertyEditor
- Navigation
- Classes
- Typedefs



---

## TedsQueryStack

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TedsQueryStack

**Contents:**
- TedsQueryStack
- Navigation
- Classes
- Interfaces
- Functions
  - Public

bool UE::Editor::DataStorage::QueryStack::operator! ( FRowQueryResultsNode::ESyncFlags E )

FRowQueryResultsNode::ESyncFlags UE::Editor::DataStorage::QueryStack::operator& ( FRowQueryResultsNode::ESyncFlags Lhs, FRowQueryResultsNode::ESyncFlags Rhs )

FRowQueryResultsNode::ESyncFlags & UE::Editor::DataStorage::QueryStack::operator&= ( FRowQueryResultsNode::ESyncFlags& Lhs, FRowQueryResultsNode::ESyncFlags Rhs )

FRowQueryResultsNode::ESyncFlags UE::Editor::DataStorage::QueryStack::operator^ ( FRowQueryResultsNode::ESyncFlags Lhs, FRowQueryResultsNode::ESyncFlags Rhs )

FRowQueryResultsNode::ESyncFlags & UE::Editor::DataStorage::QueryStack::operator^= ( FRowQueryResultsNode::ESyncFlags& Lhs, FRowQueryResultsNode::ESyncFlags Rhs )

FRowQueryResultsNode::ESyncFlags UE::Editor::DataStorage::QueryStack::operator| ( FRowQueryResultsNode::ESyncFlags Lhs, FRowQueryResultsNode::ESyncFlags Rhs )

FRowQueryResultsNode::ESyncFlags & UE::Editor::DataStorage::QueryStack::operator|= ( FRowQueryResultsNode::ESyncFlags& Lhs, FRowQueryResultsNode::ESyncFlags Rhs )

FRowQueryResultsNode::ESyncFlags UE::Editor::DataStorage::QueryStack::operator~ ( FRowQueryResultsNode::ESyncFlags E )



---

## TedsSettings

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TedsSettings

**Contents:**
- TedsSettings
- Navigation
- Classes
- Structs
- Constants



---

## TedsTableViewer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TedsTableViewer

**Contents:**
- TedsTableViewer
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Functions
  - Public

bool UE::Editor::DataStorage::CheckValidFilterQueryHandle ( const QueryHandle& InQueryHandle )



---

## TedsTypedElementBridge

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TedsTypedElementBridge

**Contents:**
- TedsTypedElementBridge
- Navigation



---

## TedsTypeInfo

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TedsTypeInfo

**Contents:**
- TedsTypeInfo
- Navigation
- Classes
- Structs
- Typedefs
- Constants



---

## TedsUI

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TedsUI

**Contents:**
- TedsUI
- Navigation
- Classes
- Structs



---

## TemplateSequence

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TemplateSequence

**Contents:**
- TemplateSequence
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## TestFramework

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TestFramework

**Contents:**
- TestFramework
- Navigation
- Classes



---

## TestSamples

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TestSamples

**Contents:**
- TestSamples
- Navigation
- Classes



---

## TetMeshing

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TetMeshing

**Contents:**
- TetMeshing
- Navigation
- Classes
- Interfaces



---

## Text3D

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/Text3D

**Contents:**
- Text3D
- Navigation
- Classes
- Structs
- Enums
  - Public
- Constants
- Variables
  - Public
- Functions

bool operator! ( EText3DRendererFlags E )

EText3DRendererFlags operator& ( EText3DRendererFlags Lhs, EText3DRendererFlags Rhs )

EText3DRendererFlags & operator&= ( EText3DRendererFlags& Lhs, EText3DRendererFlags Rhs )

EText3DRendererFlags operator^ ( EText3DRendererFlags Lhs, EText3DRendererFlags Rhs )

EText3DRendererFlags & operator^= ( EText3DRendererFlags& Lhs, EText3DRendererFlags Rhs )

EText3DRendererFlags operator| ( EText3DRendererFlags Lhs, EText3DRendererFlags Rhs )

EText3DRendererFlags & operator|= ( EText3DRendererFlags& Lhs, EText3DRendererFlags Rhs )

EText3DRendererFlags operator~ ( EText3DRendererFlags E )

AStaticMeshActor * UE::Text3D::Utilities::Conversion::ConvertToStaticMesh ( const UText3DComponent* InComponent )

bool UE::Text3D::Utilities::Conversion::PickAssetPath ( const FString& InDefaultPath, FString& OutPickedPath )

TEXT3bool UE::Text3D::Utilities::Font::GetFontFaces ( const UFont* InFont, TArray< UFontFace* >& OutFontFaces )

TEXT3bool UE::Text3D::Utilities::Font::GetFontName ( const UFont* InFont, FString& OutFontName )

TEXT3bool UE::Text3D::Utilities::Font::GetFontStyle ( const UFont* InFont, EText3DFontStyleFlags& OutFontStyleFlags )

TEXT3bool UE::Text3D::Utilities::Font::GetFontStyle ( const FText3DFontFamily& InFontFamily, EText3DFontStyleFlags& OutFontStyleFlags )

TEXT3bool UE::Text3D::Utilities::Font::GetSanitizeFontName ( const UFont* InFont, FString& OutFontName )

TEXT3void UE::Text3D::Utilities::Font::SanitizeFontName ( FString& InOutFontName )



---

## TextToSpeech

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TextToSpeech

**Contents:**
- TextToSpeech
- Navigation
- Classes
- Interfaces
- Typedefs



---

## TextureAlignMode

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TextureAlignMode

**Contents:**
- TextureAlignMode
- Navigation
- Classes



---

## TextureGraphEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TextureGraphEditor

**Contents:**
- TextureGraphEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## TextureGraphEngine

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TextureGraphEngine

**Contents:**
- TextureGraphEngine
- Navigation



---

## TextureGraphInsightEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TextureGraphInsightEditor

**Contents:**
- TextureGraphInsightEditor
- Navigation
- Classes



---

## TextureGraphInsight

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TextureGraphInsight

**Contents:**
- TextureGraphInsight
- Navigation
- Classes
- Structs
- Typedefs
- Constants
- Functions
  - Public

bool operator== ( const STextureGraphInsightDeviceListView::FItem& i, const RecordID& rid )

int32_t TiledSum ( const T_Tiled< Type >& tiles )



---

## TextureGraph

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TextureGraph

**Contents:**
- TextureGraph
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Variables
  - Public
- Functions

void FTG_LevelsSettings_VarPropertySerialize ( FTG_Var::VarPropertySerialInfo& Info )

FTG_Hash TG_Hash ( FTG_Hash H )

FTG_Hash TG_HashName ( FTG_Name& Name )

TArray< FName > TG_MakeArrayOfArgumentNames ( const FTG_Arguments& InArguments )

FName TG_MakeNameUniqueInCollection ( FName CandidateName, const TArray< FName >& Collection, FName RecursionPreFix, int32 RecursionCount )

FString TG_Var_LogValue ( FTG_LevelsSettings& Value )

FString TG_Var_LogValue ( T& Value )

FString TG_Var_LogValue ( bool& Value )

FString TG_Var_LogValue ( int& Value )

FString TG_Var_LogValue ( float& Value )

FString TG_Var_LogValue ( uint8& Value )

FString TG_Var_LogValue ( FLinearColor& Value )

FString TG_Var_LogValue ( FVector4f& Value )

FString TG_Var_LogValue ( FVector2f& Value )

FString TG_Var_LogValue ( FName& Value )

FString TG_Var_LogValue ( FString& Value )

FString TG_Var_LogValue ( TObjectPtr< UObject >& Value )

FString TG_Var_LogValue ( FTG_Texture& Value )

FString TG_Var_LogValue ( FTG_Scalar& Value )

FString TG_Var_LogValue ( FTG_OutputSettings& Value )

FString TG_Var_LogValue ( FTG_TextureDescriptor& Value )

FString TG_Var_LogValue ( FTG_Variant& Value )

FString TG_Var_LogValue ( FTG_Material& Value )

void TG_Var_SetValueFromString ( FTG_LevelsSettings& Value, const FString& StrVal )

void TG_Var_SetValueFromString ( T& Value, const FString& StrVal )

void TG_Var_SetValueFromString ( int& Value, const FString& StrVal )

void TG_Var_SetValueFromString ( bool& Value, const FString& StrVal )

void TG_Var_SetValueFromString ( float& Value, const FString& StrVal )

void TG_Var_SetValueFromString ( uint8& Value, const FString& StrVal )

void TG_Var_SetValueFromString ( TObjectPtr< UObject >& Value, const FString& StrVal )

void TG_Var_SetValueFromString ( FLinearColor& Value, const FString& StrVal )

void TG_Var_SetValueFromString ( FVector4f& Value, const FString& StrVal )

void TG_Var_SetValueFromString ( FVector2f& Value, const FString& StrVal )

void TG_Var_SetValueFromString ( FName& Value, const FString& StrVal )

void TG_Var_SetValueFromString ( FString& Value, const FString& StrVal )

void TG_Var_SetValueFromString ( FTG_Scalar& Value, const FString& StrVal )

void TG_Var_SetValueFromString ( FTG_OutputSettings& Value, const FString& StrVal )

void TG_Var_SetValueFromString ( FTG_TextureDescriptor& Value, const FString& StrVal )

void TG_Var_SetValueFromString ( FTG_Variant& Value, const FString& StrVal )

void TG_Var_SetValueFromString ( FTG_Material& Value, const FString& StrVal )



---

## TextureShareCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TextureShareCore

**Contents:**
- TextureShareCore
- Navigation
- Interfaces



---

## TextureShareDisplayCluster

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TextureShareDisplayCluster

**Contents:**
- TextureShareDisplayCluster
- Navigation
- Interfaces



---

## TextureShare

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TextureShare

**Contents:**
- TextureShare
- Navigation
- Classes
- Structs
- Interfaces



---

## Third-Party Rendering Tools and Plugins

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/third-party-rendering-tools-and-plugins-in-unreal-engine

**Contents:**
- Third-Party Rendering Tools and Plugins
- Topics

A listing of third-party tools and plugins that are available.

Unreal Engine sometimes provides integrated third-party tools and plugins that are useful for development. These may include programming tools for debugging, gathering additional information, or ones that offer hardware benefits, like support for multiple linked GPUs.



---

## TimecodeSynchronizerEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TimecodeSynchronizerEditor

**Contents:**
- TimecodeSynchronizerEditor
- Navigation
- Classes
- Interfaces
- Functions
  - Public

class UE_DEPRECATED (

class UE_DEPRECATED (



---

## TimecodeSynchronizer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TimecodeSynchronizer

**Contents:**
- TimecodeSynchronizer
- Navigation
- Classes
- Structs
- Interfaces



---

## TimedDataMonitor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TimedDataMonitor

**Contents:**
- TimedDataMonitor
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## ToolPresetAsset

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ToolPresetAsset

**Contents:**
- ToolPresetAsset
- Navigation
- Classes
- Structs



---

## ToolPresetEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ToolPresetEditor

**Contents:**
- ToolPresetEditor
- Navigation
- Classes
- Interfaces
- Variables
  - Public



---

## TraceUtilities

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TraceUtilities

**Contents:**
- TraceUtilities
- Navigation
- Classes



---

## TrajectoryTools

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TrajectoryTools

**Contents:**
- TrajectoryTools
- Navigation
- Classes
- Structs



---

## TweeningUtilsEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TweeningUtilsEditor

**Contents:**
- TweeningUtilsEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

bool UE::TweeningUtilsEditor::BlendCurve_ByKeyRange ( const FCurveEditor& InCurveEditor, const FContiguousKeyMapping& InKeySelection, TCallback&& InBlendRangeCallback )

bool UE::TweeningUtilsEditor::BlendCurves_BySingleKey ( const FCurveEditor& InCurveEditor, const FContiguousKeyMapping& InKeySelection, TCallback&& InBlendKeyCallback )

void UE::TweeningUtilsEditor::ForEachBlendFunction ( TCallback&& InCallback )

void UE::TweeningUtilsEditor::ForEachBlendFunctionBreakable ( TCallback&& InCallback )

void UE::TweeningUtilsEditor::ForEachCurveTweenable ( TCallback&& InCallback )

int32 UE::TweeningUtilsEditor::NumBlendFunctionsSupportingTweenRange()

bool UE::TweeningUtilsEditor::SupportsTweenRange ( EBlendFunction BlendFunction )

double UE::TweeningUtilsEditor::TweenRange ( double InBlendValue, const FBlendRangesData& AllBlendedKeys, const FContiguousKeys& CurrentBlendRange, int32 InCurrentKeyIndex )



---

## TweeningUtils

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/TweeningUtils

**Contents:**
- TweeningUtils
- Navigation



---

## UAFAnimGraphUncookedOnly

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UAFAnimGraphUncookedOnly

**Contents:**
- UAFAnimGraphUncookedOnly
- Navigation
- Classes
- Structs



---

## UAFAnimGraph

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UAFAnimGraph

**Contents:**
- UAFAnimGraph
- Navigation
- Classes
- Structs
- Enums
  - Public
- Variables
  - Public
- Functions
  - Public

bool operator! ( EAnimNextInjectionStatus E )

EAnimNextInjectionStatus operator& ( EAnimNextInjectionStatus Lhs, EAnimNextInjectionStatus Rhs )

EAnimNextInjectionStatus & operator&= ( EAnimNextInjectionStatus& Lhs, EAnimNextInjectionStatus Rhs )

EAnimNextInjectionStatus operator^ ( EAnimNextInjectionStatus Lhs, EAnimNextInjectionStatus Rhs )

EAnimNextInjectionStatus & operator^= ( EAnimNextInjectionStatus& Lhs, EAnimNextInjectionStatus Rhs )

EAnimNextInjectionStatus operator| ( EAnimNextInjectionStatus Lhs, EAnimNextInjectionStatus Rhs )

EAnimNextInjectionStatus & operator|= ( EAnimNextInjectionStatus& Lhs, EAnimNextInjectionStatus Rhs )

EAnimNextInjectionStatus operator~ ( EAnimNextInjectionStatus E )



---

## UAFEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UAFEditor

**Contents:**
- UAFEditor
- Navigation
- Classes
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

const FLazyName UE::UAF::Editor::CompilerResultsTabName ( "CompilerResultsTab" )

const FLazyName UE::UAF::Editor::FindAndReplaceTabName ( "FindAndReplaceTab" )

const FLazyName UE::UAF::Editor::FindTabName ( "FindTab" )

const FLazyName UE::UAF::Editor::LogListingName ( "AnimNextCompilerResults" )



---

## UAFPoseSearch

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UAFPoseSearch

**Contents:**
- UAFPoseSearch
- Navigation
- Structs



---

## UAFStateTreeEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UAFStateTreeEditor

**Contents:**
- UAFStateTreeEditor
- Navigation
- Interfaces



---

## UAFStateTreeUncookedOnly

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UAFStateTreeUncookedOnly

**Contents:**
- UAFStateTreeUncookedOnly
- Navigation
- Classes
- Structs



---

## UAFTestSuite

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UAFTestSuite

**Contents:**
- UAFTestSuite
- Navigation
- Structs



---

## UAFTests

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UAFTests

**Contents:**
- UAFTests
- Navigation
- Classes



---

## UAFUncookedOnly

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UAFUncookedOnly

**Contents:**
- UAFUncookedOnly
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

bool operator! ( EAnimNextExportedVariableFlags E )

EAnimNextExportedVariableFlags operator& ( EAnimNextExportedVariableFlags Lhs, EAnimNextExportedVariableFlags Rhs )

EAnimNextExportedVariableFlags & operator&= ( EAnimNextExportedVariableFlags& Lhs, EAnimNextExportedVariableFlags Rhs )

EAnimNextExportedVariableFlags operator^ ( EAnimNextExportedVariableFlags Lhs, EAnimNextExportedVariableFlags Rhs )

EAnimNextExportedVariableFlags & operator^= ( EAnimNextExportedVariableFlags& Lhs, EAnimNextExportedVariableFlags Rhs )

EAnimNextExportedVariableFlags operator| ( EAnimNextExportedVariableFlags Lhs, EAnimNextExportedVariableFlags Rhs )

EAnimNextExportedVariableFlags & operator|= ( EAnimNextExportedVariableFlags& Lhs, EAnimNextExportedVariableFlags Rhs )

EAnimNextExportedVariableFlags operator~ ( EAnimNextExportedVariableFlags E )



---

## UAF

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UAF

**Contents:**
- UAF
- Navigation
- Classes
- Structs
- Typedefs
- Enums
  - Public
- Variables
  - Public
- Functions

TSharedPtr< EventType, ESPMode::ThreadSafe > MakeTraitEvent ( TArgs&&... Args )



---

## UbaController

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UbaController

**Contents:**
- UbaController
- Navigation
- Classes



---

## UdpMessaging

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UdpMessaging

**Contents:**
- UdpMessaging
- Navigation
- Classes
- Interfaces
- Enums
  - Public



---

## UEOpenExrRTTI

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UEOpenExrRTTI

**Contents:**
- UEOpenExrRTTI
- Navigation
- Interfaces



---

## UIFramework

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UIFramework

**Contents:**
- UIFramework
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## UMGWidgetPreview

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UMGWidgetPreview

**Contents:**
- UMGWidgetPreview
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Variables
  - Public



---

## UnrealUSDWrapper

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UnrealUSDWrapper

**Contents:**
- UnrealUSDWrapper
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public

TSharedRef< ObjectType > MakeSharedUnreal ( ArgTypes&&... Args )

TUsdStore< UsdObjectType > MakeUsdStore ( ArgTypes&&... Args )

bool operator! ( EUsdPurpose E )

bool operator! ( EUsdDefaultKind E )

EUsdPurpose operator& ( EUsdPurpose Lhs, EUsdPurpose Rhs )

EUsdDefaultKind operator& ( EUsdDefaultKind Lhs, EUsdDefaultKind Rhs )

EUsdPurpose & operator&= ( EUsdPurpose& Lhs, EUsdPurpose Rhs )

EUsdDefaultKind & operator&= ( EUsdDefaultKind& Lhs, EUsdDefaultKind Rhs )

EUsdPurpose operator^ ( EUsdPurpose Lhs, EUsdPurpose Rhs )

EUsdDefaultKind operator^ ( EUsdDefaultKind Lhs, EUsdDefaultKind Rhs )

EUsdPurpose & operator^= ( EUsdPurpose& Lhs, EUsdPurpose Rhs )

EUsdDefaultKind & operator^= ( EUsdDefaultKind& Lhs, EUsdDefaultKind Rhs )

EUsdPurpose operator| ( EUsdPurpose Lhs, EUsdPurpose Rhs )

EUsdDefaultKind operator| ( EUsdDefaultKind Lhs, EUsdDefaultKind Rhs )

EUsdPurpose & operator|= ( EUsdPurpose& Lhs, EUsdPurpose Rhs )

EUsdDefaultKind & operator|= ( EUsdDefaultKind& Lhs, EUsdDefaultKind Rhs )

EUsdPurpose operator~ ( EUsdPurpose E )

EUsdDefaultKind operator~ ( EUsdDefaultKind E )



---

## Unreal Editor Interface

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-editor-interface

**Contents:**
- Unreal Editor Interface
- Menu Bar
- Main Toolbar
- Viewport Toolbar
- Level Viewport
- Navigating the Viewport
- Content Drawer and Content Browser
- Bottom Toolbar
- Outliner
- Details Panel

Overview of the key elements of the Unreal Editor interface

This introduction to the Unreal Engine interface describes the most common buttons, panels, and toolbars you’ll interact with in the Unreal Editor. In this page, you’ll learn more about what they do and how you can use them. While some of these elements are generally the same across various parts of the engine, you should spend some time getting familiar with their general purpose and functionality, especially if you are new to developing projects with Unreal Engine. You can also follow links throughout this page for a deeper dive into how you can use them.

When you open the engine for the first time, the Level Editor opens. This provides the core creation functionality to the Unreal Editor and is used for designing and constructing levels and environments. It is where you’ll spend most of your time developing content for your project. There are different editors in Unreal Engine used for different purposes.

Once your project opens, you will see the following layout, keeping in mind that what’s in the level will differ depending on the project you open. For this example, we are using the First Person template.

Uses these menus to access common application actions, like saving, and creating new levels. You’ll also find options for opening editor windows and tools that are useful for specific functions like debugging and more.

Contains shortcuts for some of the most common tools and editors in Unreal Engine, as well as shortcuts to enter Play mode (run your game inside Unreal Editor) and to deploy your project to other platforms.

Includes common tools used to manipulate objects in the level by moving, rotating, and scaling them, as well as snapping tools for moving objects along a grid, rotation angle, or scaling amount. It also includes perspective and orthographic views along with debugging and visualization view mode and other settings you can use while working in the viewport.

Displays the contents of your Level, such as Cameras, Actors, Static Meshes, and so on.

Displays a hierarchical tree view of all content in your Level.

Appears when you select an Actor. Displays various properties for that Actor, such as its Transform (position in the Level), Static Mesh, Material, and physics settings. This panel displays different settings depending on what you select in the Level Viewport.

Opens the Content Drawer, a temporary Content Browser window, from which you can access all of the Assets in your Project.

Contains shortcuts to the Command Console, Output Log, and Derived Data functionality. Also displays source control status.

Each editor in Unreal Engine has a menu bar that is located in the top-left of the editor window (Windows), or at the top-left of the display (macOS). Some of the menus, such as File, Window, and Help, are present in all editor windows, not just the Level Editor. Some other menus are specific to their own editors.

The Main Toolbar contains shortcuts to some of the most used tools and commands in Unreal Editor. It is divided into the following areas:

Click this button to save the level that is currently open.

Select the open level

Click this button to show the currently loaded level in the Content Browser. This will open the most recently used Content Browser, which can be the docked Content Drawer or standalone Content Browser panel.

Contains shortcuts for quickly switching between different modes to edit content within your level. These modes also change the primary behavior of the Level Editor, which can include toolbar options designed for each mode specifically. You can click the links to go to their respective pages to learn more about a mode.

Contains shortcuts for adding and opening common types of content within the Level Editor.

The Create button can be used to choose from a list of common Actor Types and Recently Used assets from the Content Browser to quickly add to your level.

The Blueprints button can be used to create and access blueprints.

The Cinematics button can be used to create and access a Level Sequence or Master Sequence cinematic.

Contains the shortcut buttons Play, Skip, Stop, and Eject for running your game in the editor.

Contains a series of options you can use to configure, prepare, and deploy your project to different platforms, such as desktop platforms such as Windows, macOS and Linux, mobile, and consoles.

Some platforms, such as mobile and console, require additional setup and configuration of your project. These can include their own software development kit (SDK) installations or non-disclosure agreements (NDAs) to access them.

The Viewport Toolbar can be used to accomplish a number of tasks when building levels. It is located at the top of the Level Viewport, and its settings and tools are grouped into the following categories:

Transform and Snapping tools

These are the options to swap between different Transform tools and change the snapping options.

These are the options to switch between Perspective and Orthographic views and change camera movement speed.

View Mode and Show Flag options

These are the options to pick between different view modes like Lit, Unlit, and Wireframe, and show flags related to the current viewport to hide and reveal types of content in the Level Viewport.

Performance and Scalability tools

This dropdown can be used to reveal settings like Viewport Scalability and Material Quality Level.

These options can be used to change viewport related settings, like mouse sensitivity in the Level Viewport.

To learn more about this toolbar, read the Viewport Toolbar documentation.

The Level Viewport displays the contents of the level that is currently loaded. When opening a project in Unreal Engine, the project's default level is loaded For example, if you open the First or Third Person Template project, you’ll see a gray box area (like the one pictured below) with some physics objects, floors, walls, and ramps.

The Level Viewport is where you can view and edit the contents of your Level, whether it's a game environment, a product visualization, or something else.

The Level Viewport can generally display the contents of the Level in two different ways:

Perspective is a 3D view you can navigate to see the contents of the viewport from different angles.

Orthographic is a 2D view that looks towards a specific direction (top, down, left, right, front, back). This creates a view where the distance from the object doesn’t affect size or provide a sense of depth.

The Viewport Type can be changed between Default Viewport and Cinematic Viewport. Default Viewport displays gizmos and icons in the level like Camera actors, Collision Components, and the World Grid.

Additionally, you can change the View Mode of your viewport by pressing the Lit button in the top-right corner of the viewport. Lit is the default view mode used for real-time applications in the Perspective view, where you can preview your scene with normally rendered lighting. If you select another View Mode, this button will be titled after that. So, if you have already selected one of the Orthographic views (Top, Front, Left, and so on), the button might say Wireframe in your viewport as that is the default View Mode for the Orthographic view. If you press it, and select Lit, you will see your environment fully lit again in any view mode.

You can use the Scalability options to change the visual fidelity of which your level is being previewed. By clicking the Performance and Scalability button and clicking Viewport Scalability, you can change to a different scalability group.

To learn more about the scalability options, see the Scalability Reference page.

Let’s explore your Level! To control the viewport camera, the perspective through which you view the Level, press and hold the Right Mouse Button (RMB) anywhere in the viewport. While holding down RMB, you can use the W, A, S, and D keys to fly through the scene. You can fly up and down with the E and Q keys.

Releasing RMB and holding down the Left Mouse Button (LMB) can be used along with dragging the mouse to move the camera forward, backward, and rotate it left or right. This provides an alternative method for navigating the environment with greater precision.

Clicking on an object in the Level with the LMB selects the object. Selected objects can be manipulated using the Transform Tool gizmos in the viewport. Gizmos are a set of on-screen handles used to move, rotate, or scale the object along specific axes, activated based on the transform tool you select. You can activate the Translate tool by pressing W, the Rotation tool by pressing E, and the Scale tool by pressing R. Alternatively, you can use the Toolbar located at the top-right of the Viewport to switch between Transform tools.

Once you have selected a tool, you can manipulate the object using the gizmo’s axes. With the Translate or Scale tools, you can also drag from the center of the gizmo to adjust all axes simultaneously. This is particularly useful for uniformly scaling an object without disproportionately affecting any single axis.

The viewport will have snapping enabled by default for every way of transforming your object. You can turn these off or change their snapping values by using the individual settings on the top-left side of the viewport.

For more information on how to navigate a level, see the Viewport Controls page.

The Content Browser is a file explorer for your project where you can organize all the assets that make up your project. These assets can include Blueprints, Geometry (static and skeletal), textures, materials, and so on.

The Content Drawer, located in the bottom-left corner of the Unreal Editor, opens a special instance of the Content Browser that automatically minimizes when it loses focus (that is, when you click away from it). To keep it open, click the Dock in Layout button in the top-right corner of the Content Drawer. This creates a new instance of the Content Browser, but you can still open a new Content Drawer. You can also open a Content Drawer by holding down CTRL key and pressing the Space key.

The Bottom Toolbar contains shortcuts and settings to various elements of the Unreal Editor. Depending on the Editor you are in (like the Viewport Editor), some of these options might not be available.

Temporary content browser window which gets dismissed as it loses focus, used for quick access.

OutputLog Drawer and Command Prompt

Opening the Output Log and entering Console Commands, including changing between executing Unreal Commands and Python scripts.

Start tracing, save a Snapshot of the Current Trace Buffer, and change Trace settings.

Provides Derived Data functionality.

Recompile and reload C++ code on the fly using Live Coding.

This option is only available in C++ projects, not Blueprint projects.

View the number of Levels with changes not yet saved. You can click on this option to view unsaved Levels.

Connect to Revision Control and View Changes, Submit Content, or Check Out Modified Files.

The Outliner panel displays a hierarchical view of all content in your level. It is located in the upper-right corner of the Unreal Editor window. You can have up to four different Outliners, each with its own column layout and filter configuration.

You can hide or reveal objects by clicking their associated Eye button. Accessing an object’s context menu can be done by right-clicking that object in the Outliner. You can then perform additional, actor-specific operations from that menu.

To keep your levels organized, you can create, move, and delete content folders. Folders can be used to group objects in your level together.

When you select an actor in the Level Viewport or the Outliner, the Details panel will show the settings and properties that affect the actor you selected. By default, it is located on the right side of the Unreal Editor window, under the Outliner panel.

As shown in the image above:

The ramp object in the Level is highlighted after being selected (clicked on).

The ramp object is also highlighted in the Outliner panel automatically. Selecting an object through the Level Viewport or the Outliner Panel highlights it the same.

The Details panel shows the components and properties of the ramp object. You can modify the properties of an object through the Details panel. To learn more about components, see the Components Window page.

You can filter the actor’s properties to view and change by selecting a specific Component at the top of the Details panel. You can lock the current selection into the Details panel, which you can use to highlight other objects while keeping the Details panel locked on the first object.



---

## UObjectPlugin

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UObjectPlugin

**Contents:**
- UObjectPlugin
- Navigation
- Classes
- Structs
- Interfaces



---

## USDClassesEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/USDClassesEditor

**Contents:**
- USDClassesEditor
- Navigation
- Interfaces
- Enums
  - Public



---

## USDClasses

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/USDClasses

**Contents:**
- USDClasses
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

ENUM_CLASS_FLAGS ( EUsdModelCardFace )

bool operator! ( EUsdReferenceMaterialProperties E )

EUsdReferenceMaterialProperties operator& ( EUsdReferenceMaterialProperties Lhs, EUsdReferenceMaterialProperties Rhs )

EUsdReferenceMaterialProperties & operator&= ( EUsdReferenceMaterialProperties& Lhs, EUsdReferenceMaterialProperties Rhs )

EUsdReferenceMaterialProperties operator^ ( EUsdReferenceMaterialProperties Lhs, EUsdReferenceMaterialProperties Rhs )

EUsdReferenceMaterialProperties & operator^= ( EUsdReferenceMaterialProperties& Lhs, EUsdReferenceMaterialProperties Rhs )

EUsdReferenceMaterialProperties operator| ( EUsdReferenceMaterialProperties Lhs, EUsdReferenceMaterialProperties Rhs )

EUsdReferenceMaterialProperties & operator|= ( EUsdReferenceMaterialProperties& Lhs, EUsdReferenceMaterialProperties Rhs )

EUsdReferenceMaterialProperties operator~ ( EUsdReferenceMaterialProperties E )

UMaterialInstanceConstant * UsdUnreal::MaterialUtils::CreateDisplayColorMaterialInstanceConstant ( const FDisplayColorMaterial& DisplayColorDescription )

UMaterialInstanceDynamic * UsdUnreal::MaterialUtils::CreateDisplayColorMaterialInstanceDynamic ( const FDisplayColorMaterial& DisplayColorDescription )

const FSoftObjectPath * UsdUnreal::MaterialUtils::GetReferenceMaterialPath ( const FDisplayColorMaterial& DisplayColorDescription )

FSoftObjectPath UsdUnreal::MaterialUtils::GetReferencePreviewSurfaceMaterial ( EUsdReferenceMaterialProperties ReferenceMaterialProperties )

const TArray< FName > & UsdUnreal::MaterialUtils::GetRegisteredRenderContexts()

FSoftObjectPath UsdUnreal::MaterialUtils::GetTwoSidedVersionOfReferencePreviewSurfaceMaterial ( const FSoftObjectPath& ReferenceMaterial )

FSoftObjectPath UsdUnreal::MaterialUtils::GetVTVersionOfReferencePreviewSurfaceMaterial ( const FSoftObjectPath& ReferenceMaterial )

bool UsdUnreal::MaterialUtils::IsReferencePreviewSurfaceMaterial ( const FSoftObjectPath& ReferenceMaterial )

void UsdUnreal::MaterialUtils::RegisterRenderContext ( const FName& RenderContextName )

void UsdUnreal::MaterialUtils::UnregisterRenderContext ( const FName& RenderContextName )

UUsdAssetImportData * UsdUnreal::ObjectUtils::GetAssetImportData ( UObject* Asset )

T * UsdUnreal::ObjectUtils::GetAssetUserData ( UObject* Object )

UUsdAssetUserData * UsdUnreal::ObjectUtils::GetAssetUserData ( const UObject* Object, TSubclassOf< UUsdAssetUserData > Class )

TSubclassOf< UUsdAssetUserData > UsdUnreal::ObjectUtils::GetAssetUserDataClassForObject ( UClass* ObjectClass )

UAssetImportData * UsdUnreal::ObjectUtils::GetBaseAssetImportData ( UObject* Asset )

T * UsdUnreal::ObjectUtils::GetOrCreateAssetUserData ( UObject* Object )

UUsdAssetUserData * UsdUnreal::ObjectUtils::GetOrCreateAssetUserData ( UObject* Object, TSubclassOf< UUsdAssetUserData > Class )

FString UsdUnreal::ObjectUtils::GetPrefixedAssetName ( const FString& DesiredName, UClass* AssetClass )

FString UsdUnreal::ObjectUtils::GetUniqueName ( FString Name, const StringContainer& UsedNames )

bool UsdUnreal::ObjectUtils::RemoveNumberedSuffix ( FString& Prefix )

FString UsdUnreal::ObjectUtils::SanitizeObjectName ( const FString& InObjectName )

void UsdUnreal::ObjectUtils::SetAssetImportData ( UObject* Asset, UAssetImportData* ImportData )

bool UsdUnreal::ObjectUtils::SetAssetUserData ( UObject* Object, UUsdAssetUserData* AssetUserData )

void UsdUtils::AddAnalyticsAttributes ( const FUsdMetadataImportOptions& Options, TArray< FAnalyticsEventAttribute >& InOutAttributes )

void UsdUtils::AddAnalyticsAttributes ( const FUsdStageOptions& Options, TArray< FAnalyticsEventAttribute >& InOutAttributes )

EUsdModelCardFace UsdUtils::GetOppositeFaceOnSameAxis ( EUsdModelCardFace Face )

void UsdUtils::HashForExport ( const FUsdStageOptions& Options, FSHA1& HashToUpdate )

void UsdUtils::HashForImport ( const FUsdMetadataImportOptions& Options, FSHA1& HashToUpdate )



---

## USDExporter

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/USDExporter

**Contents:**
- USDExporter
- Navigation
- Classes
- Structs
- Interfaces



---

## USDImporterMDL

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/USDImporterMDL

**Contents:**
- USDImporterMDL
- Navigation



---

## USDSchemas

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/USDSchemas

**Contents:**
- USDSchemas
- Navigation
- Interfaces
- Functions
  - Public

void UsdUnreal::Analytics::CollectSchemaAnalytics ( const UE::FUsdStage& Stage, const FString& EventName )



---

## USDStageEditorViewModels

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/USDStageEditorViewModels

**Contents:**
- USDStageEditorViewModels
- Navigation
- Classes
- Interfaces
- Typedefs
- Enums
  - Public
- Variables
  - Public



---

## USDStageEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/USDStageEditor

**Contents:**
- USDStageEditor
- Navigation
- Classes
- Interfaces



---

## USDStageImporter

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/USDStageImporter

**Contents:**
- USDStageImporter
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

void UsdUtils::AddAnalyticsAttributes ( const UUsdStageImportOptions& Options, TArray< FAnalyticsEventAttribute >& InOutAttributes )



---

## USDStage

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/USDStage

**Contents:**
- USDStage
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Variables
  - Public



---

## USDUtilities

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/USDUtilities

**Contents:**
- USDUtilities
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

void UsdUnreal::ExportUtils::BeginUniquePathScope ()

void UsdUnreal::ExportUtils::EndUniquePathScope ()

FString UsdUnreal::ExportUtils::GetUniqueFilePathForExport ( const FString& DesiredPathWithExtension )

void UsdUnreal::ExportUtils::SanitizeFilePath ( FString& Path )



---

## UserToolBoxBasicCommand

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UserToolBoxBasicCommand

**Contents:**
- UserToolBoxBasicCommand
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## UserToolBoxCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UserToolBoxCore

**Contents:**
- UserToolBoxCore
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## UVEditorToolsEditorOnly

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UVEditorToolsEditorOnly

**Contents:**
- UVEditorToolsEditorOnly
- Navigation
- Classes



---

## UVEditorTools

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UVEditorTools

**Contents:**
- UVEditorTools
- Navigation
- Classes
- Structs
- Interfaces
- Enums
  - Public
- Functions
  - Public

bool operator! ( ESelectionChangeTypeFlag E )

ESelectionChangeTypeFlag operator& ( ESelectionChangeTypeFlag Lhs, ESelectionChangeTypeFlag Rhs )

ESelectionChangeTypeFlag & operator&= ( ESelectionChangeTypeFlag& Lhs, ESelectionChangeTypeFlag Rhs )

ESelectionChangeTypeFlag operator^ ( ESelectionChangeTypeFlag Lhs, ESelectionChangeTypeFlag Rhs )

ESelectionChangeTypeFlag & operator^= ( ESelectionChangeTypeFlag& Lhs, ESelectionChangeTypeFlag Rhs )

ESelectionChangeTypeFlag operator| ( ESelectionChangeTypeFlag Lhs, ESelectionChangeTypeFlag Rhs )

ESelectionChangeTypeFlag & operator|= ( ESelectionChangeTypeFlag& Lhs, ESelectionChangeTypeFlag Rhs )

ESelectionChangeTypeFlag operator~ ( ESelectionChangeTypeFlag E )

PREDECLARE_GEOMETRY ( FUVEditorDynamicMeshSelection )

PREDECLARE_GEOMETRY ( FDynamicMesh3 )

PREDECLARE_GEOMETRY ( FDynamicMesh3 )

PREDECLARE_GEOMETRY ( FDynamicMesh3 )

PREDECLARE_GEOMETRY ( FUVToolSelection )

PREDECLARE_GEOMETRY ( FDynamicMesh3 )

PREDECLARE_GEOMETRY ( FDynamicMeshChange )

PREDECLARE_GEOMETRY ( FDynamicMesh )

PREDECLARE_USE_GEOMETRY_CLASS ( FDynamicMesh3 )

FAnalyticsEventAttribute UE::Geometry::UVEditorAnalytics::AnalyticsEventAttributeEnum ( const FString& AttributeName, EnumType EnumValue )



---

## UVEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/UVEditor

**Contents:**
- UVEditor
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## VariantManagerContentEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/VariantManagerContentEditor

**Contents:**
- VariantManagerContentEditor
- Navigation
- Classes
- Interfaces
- Typedefs
- Enums
  - Public



---

## VariantManagerContent

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/VariantManagerContent

**Contents:**
- VariantManagerContent
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

ENUM_CLASS_FLAGS ( EPropertyValueCategory )

UTexture2D * ThumbnailGenerator::GenerateThumbnailFromCamera ( UObject* WorldContextObject, const FTransform& CameraTransform, float FOVDegrees, float MinZ, float Gamma )

UTexture2D * ThumbnailGenerator::GenerateThumbnailFromEditorViewport()

UTexture2D * ThumbnailGenerator::GenerateThumbnailFromFile ( FString FilePath )

UTexture2D * ThumbnailGenerator::GenerateThumbnailFromObjectThumbnail ( UObject* Object )

UTexture2D * ThumbnailGenerator::GenerateThumbnailFromTexture ( UTexture2D* InImage )



---

## VariantManager

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/VariantManager

**Contents:**
- VariantManager
- Navigation
- Classes
- Structs
- Interfaces



---

## VCamCoreEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/VCamCoreEditor

**Contents:**
- VCamCoreEditor
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs



---

## VCamCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/VCamCore

**Contents:**
- VCamCore
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public
- Functions
  - Public

TArray< FName > UE::VCamCore::ConnectionUtils::FindCompatibleModifierNames ( const FVCamConnection& Connection, UVCamComponent& Component )

void UE::VCamCore::ConnectionUtils::ForEachCompatibleConnectionPoint ( const FVCamConnection& Connection, UVCamComponent& Component, FCompatibleModifierCallback ProcessConnectionPoint )

void UE::VCamCore::ForEachWidgetToConsiderForVCam ( UUserWidget& Widget, TFunctionRef< void(UWidget*)> Callback )

bool UE::VCamCore::operator! ( ENameGenerationFlags E )

ENameGenerationFlags UE::VCamCore::operator& ( ENameGenerationFlags Lhs, ENameGenerationFlags Rhs )

ENameGenerationFlags & UE::VCamCore::operator&= ( ENameGenerationFlags& Lhs, ENameGenerationFlags Rhs )

ENameGenerationFlags UE::VCamCore::operator^ ( ENameGenerationFlags Lhs, ENameGenerationFlags Rhs )

ENameGenerationFlags & UE::VCamCore::operator^= ( ENameGenerationFlags& Lhs, ENameGenerationFlags Rhs )

ENameGenerationFlags UE::VCamCore::operator| ( ENameGenerationFlags Lhs, ENameGenerationFlags Rhs )

ENameGenerationFlags & UE::VCamCore::operator|= ( ENameGenerationFlags& Lhs, ENameGenerationFlags Rhs )

ENameGenerationFlags UE::VCamCore::operator~ ( ENameGenerationFlags E )

int32 UE::VCamCore::ViewportIdToOrdinality ( EVCamTargetViewportID TargetViewport )

FString UE::VCamCore::ViewportIdToString ( EVCamTargetViewportID TargetViewport )



---

## VCamExtensions

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/VCamExtensions

**Contents:**
- VCamExtensions
- Navigation
- Classes
- Structs



---

## VertexDeltaModelEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/VertexDeltaModelEditor

**Contents:**
- VertexDeltaModelEditor
- Navigation
- Classes



---

## VertexDeltaModel

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/VertexDeltaModel

**Contents:**
- VertexDeltaModel
- Navigation
- Classes
- Variables
  - Public
  - Protected
- Functions
  - Public

void UE::VertexDeltaModel::AllocateResources ( FRDGBuilder& GraphBuilder, FAllocationData const& InAllocationData )

void UE::VertexDeltaModel::GatherDispatchData ( FDispatchData const& InDispatchData )

TArray< FVector3f > & UE::VertexDeltaModel::GetGroundTruthPositions()

virtual void UE::VertexDeltaModel::HandleZeroGroundTruthPositions()

bool UE::VertexDeltaModel::IsValid ( FValidationData const& InValidationData ) const



---

## VideoLiveLinkDeviceCommon

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/VideoLiveLinkDeviceCommon

**Contents:**
- VideoLiveLinkDeviceCommon
- Navigation
- Classes
- Structs



---

## VirtualCamera

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/VirtualCamera

**Contents:**
- VirtualCamera
- Navigation
- Classes
- Structs
- Enums
  - Public



---

## VirtualHeightfieldMesh

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/VirtualHeightfieldMesh

**Contents:**
- VirtualHeightfieldMesh
- Navigation
- Classes
- Structs



---

## Working with Plugins

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine

**Contents:**
- Working with Plugins
- Enabling a Plugin
- Disabling a Plugin
- Installing Plugins from Fab
  - Downloading Plugins from Fab
    - Free Plugin
    - Paid Plugin
    - Install your Plugin
  - Downloading Plugins From Fab Inside Unreal Engine
- Plugin Installation Locations

Installing, enabling, and disabling plugins in Unreal Engine

A plugin is an optional software component that adds specific functionality to Unreal Engine. Plugins can add entirely new features and modify built-in functionality without modifying the Unreal Engine code directly. For example, a plugin might add new menu items and toolbar commands to the editor, or even add entirely new features and editor sub-modes.

You can enable or disable plugins independently for each project, depending on your needs.

There are two types of plugins available in Unreal Engine:

Unreal Engine plugins.

To enable an Unreal Engine plugin, follow these steps:

From the main menu, go to Edit > Plugins. This opens the Plugins window.

Find the plugin you want to enable using the list on the left of the screen. Alternatively, enter a term in the Search box to search for all plugin names and descriptions that contain this term.

To enable a plugin, click the checkbox next to it.

For plugins that are not production-ready, such as beta plugins, you might see a warning asking you to confirm that you want to enable that plugin.

Save your work, then restart Unreal Engine.

Third-party plugins might require additional steps before you can enable them. For more information, refer to the documentation for the third-party plugin you want to install. Note that Epic Games is not responsible for the contents of third-party plugins.

To disable a plugin, follow these steps:

From the main menu, go to Edit > Plugins. This opens the Plugins window.

Find the plugin you want to disable using the list on the left of the screen. Alternatively, enter a term in the Search box to search for all plugin names and descriptions that contain this term.

To disable a plugin, clear the checkbox next to it.

If the plugin you want to disable is a dependency for other plugins (that is, other plugins require it to function), you will see a notification asking you if you want to disable those plugins as well. Note that this might break existing functionality in your project if you used any of those plugins to implement it.

Save your work, then restart Unreal Engine.

While Unreal Engine contains plugins that offer many different kinds of functionality, you can also install additional plugins from Fab, using the methods described below. The examples shown here use the free glTF Exporter plugin by Epic Games.

You can browse and download plugins for Unreal Engine directly from the Fab site, or from the Fab tab in the Epic Games Launcher.

To download plugins from the site, follow these steps:

Do either of the following:

In the Epic Games Launcher, navigate to the Fab tab.

Go to the Fab website.

Search for the plugin you want to install and click the thumbnail to open the listing.

The next step depends on whether you selected a free plugin or a paid plugin.

The following information is adapted from the Acquiring Products section of the Purchasing and Downloading Products page in the Fab documentation. Refer to that page for more information.

To download a free plugin, follow these steps:

On the plugin's listing click Add to My Library.

Your free plugin is now available in your Fab library on the Fab site and in the Epic Games launcher.

To download a plugin for sale, follow these steps:

Click the Select a License dropdown to view the available licenses. Select a license type if applicable. This can vary depending on the size of your organization.

Select either Buy now or Add to cart.

If you select Buy now, you are shown the checkout screen where you can pay for your selected plugin directly. Go to step 4.

If you select Add to cart, your plugin is added to your cart. Continue to step 3.

Click View in cart, then click the Checkout button to pay for your selections once you have all the plugins (and any other Fab products) you want to buy.

Complete the checkout process, and you will see the same notification as for free plugins.

After you have added your new plugin to your Fab library, you need to install it to Unreal Engine.

Go to the Library tab in the launcher, then scroll down to the Fab Library section. Search for your new plugin, then click Install to Engine.

If you can't find your new plugin, refresh the Fab Library.

Select the engine version for the plugin installation, then click Install.

When installing a plugin or other asset, only supported versions of Unreal Engine are available, even if you have other Unreal Engine versions installed.

After the installation completes, open the version of Unreal Engine you installed the plugin for, and enable the plugin following the instructions in the Enabling a Plugin section on this page.

You can download plugins (and other content) using the Fab plugin while you are working inside Unreal Engine. Before you can install additional plugins from Fab, you must first enable the Fab plugin.

After you install the plugin, you can access it from the following options in Unreal Engine:

In the Windows menu, scroll down to the Get Content section and click Fab.

In the Content Drawer, click the Fab button right next to the +Add button.

In the Fab window, you can search for and acquire plugins (both free or paid) in the same way as on the Fab site.

Only plugins usable with Unreal Engine appear in the Fab window inside Unreal Engine. Content for other platforms is not available.

After you add a plugin to your library, you must download and install it to use it. To install your new plugin, quit out of Unreal Engine, and find the plugin in your Fab Library. Click Install to Engine, and proceed as previously described above.

Unreal Engine stores all plugins at the following locations:

C:\Program Files\Epic Games\UE_[version]\Engine\Plugins on Windows

/Users/Shared/Epic Games/UE_[version]/Engine/Plugins on macOS



---
