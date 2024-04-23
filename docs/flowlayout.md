# Jetpack Compose Flow Layouts

[![Maven Central](https://img.shields.io/maven-central/v/com.google.accompanist/accompanist-flowlayout)](https://search.maven.org/search?q=g:com.google.accompanist)

!!! warning
    **This library is deprecated, with official FlowLayout support in androidx.compose.foundation.** The migration guide and original documentation is below.

## Migration Guide to the official FlowLayouts

The official `androidx.compose.foundation` FlowLayouts support is very similar to accompanist/flowlayouts, with a few changes.

1. Replace import packages to point to Androidx.Compose
``` kotlin
import androidx.compose.foundation.layout.FlowColumn
```
  
``` kotlin
import androidx.compose.foundation.layout.FlowRow
```
  
For `FlowColumn`:  

2. Replace Modifier `mainAxisAlignment` with `verticalArrangement` 

3. Replace Modifier `crossAxisAlignment` with `horizontalArrangement`

  
For `FlowRow`  

4. `mainAxisAlignment` is now `horizontalArrangement`  

5. `crossAxisAlignment` is now `verticalArrangement`  

``` kotlin
FlowColumn(
    modifier = Modifier,
    verticalArrangement = Arrangement.Top,
    horizontalArrangement = Arrangement.Start,
    content = { // columns }
) 
```
  
``` kotlin
FlowRow(
    modifier = Modifier,
    horizontalArrangement = Arrangement.Start,
    verticalArrangement = Arrangement.Top,
    content = { // rows }
) 
```
  
6. Replace `mainAxisSpacing` with `HorizontalArrangement.spacedBy(50.dp, Alignment.*)` in `FlowRow` and `VerticalArrangement.spacedBy(50.dp, Alignment.*)` in `FlowColumn`.

7. Replace `crossAxisSpacing` with `VerticalArrangement.spacedBy(50.dp, Alignment.*)` in `FlowRow` and `HorizontalArrangement.spacedBy(50.dp)` in `FlowColumn`. 

Here `Alignment.*` is the Alignment you wish to use such as `Alignment.Start`, `Alignment.Top` etc

  
``` kotlin
FlowRow(
    modifier = Modifier,
    horizontalArrangement = Arrangement.spacedBy(50.dp, Alignment.Start),
    verticalArrangement = Arrangement.spacedBy(50.dp, Alignment.Top),
    content = { // rows }
)
```

``` kotlin
FlowColumn(
    modifier = Modifier,
    verticalArrangement = Arrangement.spacedBy(50.dp, Alignment.Top),
    horizontalArrangement = Arrangement.spacedBy(50.dp, Alignment.Start),
    content = { // columns }
)
```
  
8. `lastLineMainAxisAlignment` is currently not supported in Compose Flow Layouts.

### New Features: 
#### Add weights to each child
To scale an item based on the size of its parent and the space available, adding weights is helpful. 
Adding a weight in `FlowRow` and `FlowColumn` is different than in `Row` and `Column`.

In `FlowLayout`, it is based on the number of items placed on the row it falls on and their weights. 
First we check to see if an item can fit in the current row or column based on its intrinsic size. 
If it fits and has a weight, its final size is expanded based on the available space and the number of items 
with weights placed on the row or column it falls on. 

Because of the nature of `FlowLayouts` an item only expands and does not shrink in size. Its width in `FlowRow`
or height in `FlowColumn` determines it minimum width or height, and then expands based on its weight and 
the available space remaining after row items' width/height have been determined.

``` kotlin
FlowRow() { 
     repeat(20) { Box(Modifier.size(20.dp).weight(1f, true) } 
}
```

#### Create a maximum number of items in row or column
You may choose to limit the number of items that appear in each row in `FlowRow` or column in `FlowColumn`
This can be configured using `maxItemsInEachRow` or `maxItemsInEachColumn`: 
``` kotlin
FlowRow(maxItemsInEachRow = 3) { 
     repeat(10) { Box(Modifier.size(20.dp).weight(1f, true) } 
}
```

## Examples

For examples, refer to the [Flow Row samples](https://android.googlesource.com/platform/frameworks/support/+/refs/heads/androidx-main/compose/foundation/foundation-layout/samples/src/main/java/androidx/compose/foundation/layout/samples/FlowRowSample.kt) 
and the [Flow Column samples](https://android.googlesource.com/platform/frameworks/support/+/refs/heads/androidx-main/compose/foundation/foundation-layout/samples/src/main/java/androidx/compose/foundation/layout/samples/FlowColumnSample.kt).

## Original Docs

It is most similar to `Row` and `Column` and shares similar modifiers and the scopes. 
Unlike the standard `Row` and `Column` composables, if it runs out of space on the current row, 
the children are placed in the next line, and this repeats until the children are fully placed.

## Usage
  
``` kotlin
FlowRow {
    // row contents
}

FlowColumn {
    // column contents
}
```

## Download

[![Maven Central](https://img.shields.io/maven-central/v/com.google.accompanist/accompanist-flowlayout)](https://search.maven.org/search?q=g:com.google.accompanist)

```groovy
repositories {
    mavenCentral()
}

dependencies {
    implementation "com.google.accompanist:accompanist-flowlayout:<version>"
}
```

Snapshots of the development version are available in [Sonatype's `snapshots` repository][snap]. These are updated on every commit.

[compose]: https://developer.android.com/jetpack/compose
[snap]: https://oss.sonatype.org/content/repositories/snapshots/com/google/accompanist/accompanist-flowlayout/
