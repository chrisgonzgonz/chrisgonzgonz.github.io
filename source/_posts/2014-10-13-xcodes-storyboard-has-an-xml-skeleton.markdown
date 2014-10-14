---
layout: post
title: "Xcode's Storyboard Has an XML Skeleton"
date: 2014-10-13 23:02
comments: true
categories: Xcode, iOS, Storyboard, XML
---

##Storyboard's Skeleton: XML
If you've just started dabbling in iOS and have been lucky enough to avoid Storyboard merge conflicts, you might not have run into this yet. The Storyboard file in Interface Builder is a magical place free of the HTML and CSS drudgery. It's a place where you can drag-and-drop objects into scenes as quickly as your imagination can conjure them up. But Storyboard isn't all magic; it's magic and XML.

To see how Storyboard objects translate into XML, I've put together a little Halloween themed jukebox layout:

!["monster_mash_full"](/images/monster_mash_full.png)

###Monster Mash Jukebox

Let's talk about the layout first. Our Storyboard's Initial View Controller is a standard UINavigation Controller. That UINavigation Controller has an FISJukeboxViewController as its Root View Controller. 

FISJukeboxViewController has some subviews:

* A navigation item title
* 2 UIBarButtonItems
* 2 UIButtons
* A UITextField
* A UITextView
* And A UIView "container" with 3 subviews:
	* A UISlider
	* A UIImageView
	* A UISwitch

The little magnifying glass button also has a segue action connecting it to the Song Detail View (that happens to only be host to a spooky PNG).

!["monster_mash_annotated"](/images/monster_mash_annotated.png)

###UINavigationController

Awesome! Now that we've seen our Storyboard represented both visually and described textually, let's see how it looks in a little Extensible Markup Language:

* So our UINavigationController looks like this:

```xml
    <!--Navigation Controller-->
        <scene sceneID="BAt-Fk-3mT">
            <objects>
                <navigationController automaticallyAdjustsScrollViewInsets="NO" id="qTf-YL-Hik" sceneMemberID="viewController">
                    <toolbarItems/>
                    <navigationBar key="navigationBar" contentMode="scaleToFill" id="ngq-Y5-BSZ">
                        <rect key="frame" x="0.0" y="0.0" width="320" height="44"/>
                        <autoresizingMask key="autoresizingMask"/>
                    </navigationBar>
                    <nil name="viewControllers"/>
                    <connections>
                        <segue destination="vXZ-lx-hvc" kind="relationship" relationship="rootViewController" id="mFC-jE-bus"/>
                    </connections>
                </navigationController>
                <placeholder placeholderIdentifier="IBFirstResponder" id="g6X-lG-9hB" userLabel="First Responder" sceneMemberID="firstResponder"/>
            </objects>
            <point key="canvasLocation" x="287" y="-370"/>
        </scene>
```

As you can see, it's a plain vanilla UINavigationController. The great customization of the nav bars in the following scenes will be a function of their UINavigationItems.

###FISJukeBoxViewController

```xml

<!--Monster Mash Jukebox-->
        <scene sceneID="ufC-wZ-h7g">
            <objects>
                <viewController id="vXZ-lx-hvc" customClass="FISJukeboxViewController" sceneMemberID="viewController">
                    <layoutGuides>
                        <viewControllerLayoutGuide type="top" id="jyV-Pf-zRb"/>
                        <viewControllerLayoutGuide type="bottom" id="2fi-mo-0CV"/>
                    </layoutGuides>
                    <view key="view" contentMode="scaleToFill" id="kh9-bI-dsS">
                        <rect key="frame" x="0.0" y="0.0" width="320" height="568"/>
                        <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                        <subviews>
                            <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="mf4-v3-4l3">
                                <rect key="frame" x="20" y="84" width="57" height="30"/>
                                <state key="normal" title="Play">
                                    <color key="titleShadowColor" white="0.5" alpha="1" colorSpace="calibratedWhite"/>
                                </state>
                                <connections>
                                    <action selector="playButtonTapped:" destination="vXZ-lx-hvc" eventType="touchUpInside" id="Oj5-ck-UTU"/>
                                </connections>
                            </button>
                            <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="4iq-tG-pLm">
                                <rect key="frame" x="248" y="84" width="52" height="30"/>
                                <state key="normal" title="Stop">
                                    <color key="titleShadowColor" white="0.5" alpha="1" colorSpace="calibratedWhite"/>
                                </state>
                                <connections>
                                    <action selector="stopButtonTapped:" destination="vXZ-lx-hvc" eventType="touchUpInside" id="gKe-8S-iZF"/>
                                </connections>
                            </button>
                            <textField opaque="NO" clipsSubviews="YES" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="left" contentVerticalAlignment="center" borderStyle="roundedRect" placeholder="Song #" minimumFontSize="17" translatesAutoresizingMaskIntoConstraints="NO" id="5zs-Oa-X6P">
                                <rect key="frame" x="85" y="84" width="155" height="30"/>
                                <fontDescription key="fontDescription" type="system" pointSize="14"/>
                                <textInputTraits key="textInputTraits" keyboardType="numberPad"/>
                            </textField>
                            <view contentMode="scaleToFill" fixedFrame="YES" translatesAutoresizingMaskIntoConstraints="NO" id="88c-gR-8Xt">
                                <rect key="frame" x="37" y="387" width="251" height="137"/>
                                <subviews>
                                    <imageView userInteractionEnabled="NO" contentMode="scaleToFill" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" image="halloween236.png" translatesAutoresizingMaskIntoConstraints="NO" id="Hah-IK-733">
                                        <rect key="frame" x="167" y="53" width="64" height="64"/>
                                    </imageView>
                                    <switch opaque="NO" contentMode="scaleToFill" horizontalHuggingPriority="750" verticalHuggingPriority="750" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" on="YES" translatesAutoresizingMaskIntoConstraints="NO" id="Fxc-hA-oDz">
                                        <rect key="frame" x="20" y="69" width="51" height="31"/>
                                    </switch>
                                    <slider opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" value="0.5" minValue="0.0" maxValue="1" translatesAutoresizingMaskIntoConstraints="NO" id="s6K-YA-5Nw">
                                        <rect key="frame" x="66" y="21" width="118" height="31"/>
                                    </slider>
                                </subviews>
                                <color key="backgroundColor" red="1" green="0.80000001190000003" blue="0.40000000600000002" alpha="1" colorSpace="calibratedRGB"/>
                            </view>
                            <textView clipsSubviews="YES" multipleTouchEnabled="YES" contentMode="scaleToFill" fixedFrame="YES" editable="NO" selectable="NO" translatesAutoresizingMaskIntoConstraints="NO" id="XV6-Sv-WQZ">
                                <rect key="frame" x="20" y="147" width="280" height="211"/>
                                <color key="backgroundColor" red="1" green="1" blue="1" alpha="1" colorSpace="calibratedRGB"/>
                                <mutableString key="text">Lorem ipsum dolor sit er elit lamet, consectetaur cillium adipisicing pecu, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Nam liber te conscient to factor tum poen legum odioque civiuda.</mutableString>
                                <fontDescription key="fontDescription" type="system" pointSize="14"/>
                                <textInputTraits key="textInputTraits" autocapitalizationType="sentences"/>
                            </textView>
                        </subviews>
                        <color key="backgroundColor" white="1" alpha="1" colorSpace="custom" customColorSpace="calibratedWhite"/>
                    </view>
                    <toolbarItems/>
                    <navigationItem key="navigationItem" title="Monster Mash Jukebox" id="oeF-Q3-RQ7">
                        <barButtonItem key="leftBarButtonItem" systemItem="fastForward" id="mEm-xQ-80B"/>
                        <barButtonItem key="rightBarButtonItem" systemItem="search" id="Wnw-xL-1xa">
                            <connections>
                                <segue destination="sFH-Ra-eR6" kind="push" id="dPq-Kt-AS5"/>
                            </connections>
                        </barButtonItem>
                    </navigationItem>
                    <simulatedToolbarMetrics key="simulatedBottomBarMetrics"/>
                    <connections>
                        <outlet property="playlistView" destination="XV6-Sv-WQZ" id="XGy-na-K6i"/>
                        <outlet property="songSelectorField" destination="5zs-Oa-X6P" id="Dgx-lp-xjs"/>
                    </connections>
                </viewController>
                <placeholder placeholderIdentifier="IBFirstResponder" id="x5A-6p-PRh" sceneMemberID="firstResponder"/>
            </objects>
            <point key="canvasLocation" x="669" y="-370"/>
        </scene>

```

Ok, so I know this is a lot of XML. But it's pretty cool, because if you can get past how horrible it is to read, you can see that it's SUPER DESCRIPTIVE. Like so descriptive that every little checkbox and field and setting and doohickey that appears in Xcode's Attributes Inspector, Size Inspector, Connections Inspector, and Identity Inspector for every single view and subview is represented.
