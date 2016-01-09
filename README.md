# Xnapshot
Xnapshot - automating screenshots of your iOS app on every device using Xamarin.UITest

## tl;dr

- Create an [awesome iOS app](https://itunes.apple.com/no/app/id953899091?at=11l5UV&ct=website) using C# and Xamarin. 
- Add a new ‘Console’-project to your solution and add the `Xnapshot` and [Xamarin.UITest](https://www.nuget.org/packages/Xamarin.UITest/) nuget packages. 
- Create a new class, `AppNameScreenshots` and derive from the [Xnapshot.Screenshots](https://github.com/Sankra/Xnapshot/blob/master/Xnapshot/Screenshots.cs) abstract class.
- Add your preferred device type, iOS version, screenshots folder and path to your App bundle as constructor arguments. See Usage below for allowed values.

```cs
public class GoldenRatioScreenshots : Screenshots {
  public GoldenRatioScreenshots() : base(DeviceType.iPhone,
    "iOS-9-2", 
		"/Users/sankra/Projects/GoldenRatioCalculator/screenshots/en-US", 
		"/Users/sankra/Projects/GoldenRatioCalculator/iOS/bin/iPhoneSimulator/Debug/GoldenRatioCalculatoriOS.app") {
	}
}
```

- Use Xamarin.UITest to implement the `SetAppStateForScreenshotX` methods. This should automate your app, putting it in the correct state for each screenshot. 

```cs
// Example from Golden Ratio Calculator.
// The first screenshot is of the first screen,
// thus this method is empty.
protected override void SetAppStateForScreenshot1() {
}

protected override void SetAppStateForScreenshot2() {
  App.Tap(c => c.Marked("ratioPicker"));
  App.Tap(v => v.Text("Silver Ratio"));
  App.Tap(c => c.Marked("Done"));
}

protected override void SetAppStateForScreenshot3() {
  App.Tap(c => c.Marked("ratioPicker"));
  App.Tap(v => v.Text("Bronze Ratio"));
  App.Tap(c => c.Marked("Done"));
}

protected override void SetAppStateForScreenshot4() {
  App.Tap(c => c.Marked("ratioPicker"));
  App.Tap(v => v.Text("Yamato Ratio"));
  App.Tap(c => c.Marked("Done"));
  App.Tap(c => c.Marked("rotateButton"));
}

protected override void SetAppStateForScreenshot5() {
  App.Tap(c => c.Marked("Cog.png"));
}
```

- Call the `TakeScreenshots()` method of your class and run your console app to take the screenshots.

```cs
public static void Main(string[] args) {
  var screenshots = new GoldenRatioScreenshots();
  screenshots.TakeScreenshots();

  Environment.Exit(0);
}
```

The screenshots look like this after the console app has run:



And the screenshots folder contains screenshots for all configured devices:



## Usage

## Advanced Options