Silverlight-Toolbar
===================

GUI component (C#, xaml) for Esri web maps viewer (Silverlight). Component name is **ESRI.ArcGIS.Client.Toolkit.Toolbar**

2012-11-12

Source: ArcGIS Silverlight Toolkit Toolbar from http://esrisilverlight.codeplex.com/releases/view/60154

As you may know, ESRI.ArcGIS.Client.Toolkit.Toolbar was deprecated in Toolkit v2.3 and eliminated in v3.0,
but some people (including me) still need this toolbar.
So, I downloaded ArcGIS Silverlight Toolkit v2.2 sources and extracted Toolbar component and make standalone lib.

This is it - Toolbar only lib from ESRI.ArcGIS.Client.Toolkit.
Sources included.

How to use
----------

Add ESRI.ArcGIS.Client.Toolkit.Toolbar.dll to References in your project.
If you're not using Silverlight v5 32-bit, you have to compile lib from sources.

In app layout xaml file write code for toolbar like this

```
<UserControl
...
	xmlns:tkit="clr-namespace:ESRI.ArcGIS.Client.Toolkit;assembly=ESRI.ArcGIS.Client.Toolkit.Toolbar"
...
<Canvas x:Name="VGraphicsTools" Visibility="Collapsed"
    Width="300" Height="100" HorizontalAlignment="Left" VerticalAlignment="Bottom" Margin="15,0,0,-190">
    <Rectangle Stroke="Gray"  RadiusX="10" RadiusY="10" Fill="#77919191" Canvas.Left="0"
        Canvas.Top="0" Width="300" Height="90" >
        <Rectangle.Effect>
            <DropShadowEffect/>
        </Rectangle.Effect>
    </Rectangle>
    <Rectangle Fill="#FFFFFFFF" Stroke="DarkGray" RadiusX="5" RadiusY="5" Canvas.Left="10"
        Canvas.Top="10" Width="280" Height="70"  />
	<tkit:Toolbar x:Name="VGraphicsToolbar" MaxItemHeight="80" MaxItemWidth="80"
		VerticalAlignment="Top" HorizontalAlignment="Center"
		Width="270" Height="80">
		<tkit:Toolbar.Items>
			<tkit:ToolbarItemCollection>
				<tkit:ToolbarItem Text="Add a point">
					<tkit:ToolbarItem.Content>
						<Image Source="/Images/toolbar/DrawPoint.png" Stretch="UniformToFill" Margin="5" />
					</tkit:ToolbarItem.Content>
				</tkit:ToolbarItem>
				<tkit:ToolbarItem Text="Add a Polyline">
					<tkit:ToolbarItem.Content>
						<Image Source="/Images/toolbar/DrawPolyline.png" Stretch="UniformToFill" Margin="5" />
					</tkit:ToolbarItem.Content>
				</tkit:ToolbarItem>
				<tkit:ToolbarItem Text="Add a Polygon">
					<tkit:ToolbarItem.Content>
						<Image Source="/Images/toolbar/DrawPolygon.png" Stretch="UniformToFill" Margin="5" />
					</tkit:ToolbarItem.Content>
				</tkit:ToolbarItem>
				<tkit:ToolbarItem Text="Add a Text">
					<tkit:ToolbarItem.Content>
						<Image Source="/Images/toolbar/DrawText.png" Stretch="UniformToFill" Margin="5" />
					</tkit:ToolbarItem.Content>
				</tkit:ToolbarItem>
			</tkit:ToolbarItemCollection>
		</tkit:Toolbar.Items>
	</tkit:Toolbar>
</Canvas>
```

And use this toolbar in your program like this (C#)

```
var tb = MapApplication.Current.FindObjectInLayout("VGraphicsToolbar") as ESRI.ArcGIS.Client.Toolkit.Toolbar;
tb.ToolbarItemClicked += new ESRI.ArcGIS.Client.Toolkit.ToolbarIndexChangedHandler(VGR_ToolbarItemClicked);
tb.ToolbarIndexChanged += new ESRI.ArcGIS.Client.Toolkit.ToolbarIndexChangedHandler(VGR_ToolbarIndexChanged);
tb.Visibility = Visibility.Visible;

private void VGR_ToolbarItemClicked(object sender, ESRI.ArcGIS.Client.Toolkit.SelectedToolbarItemArgs e) {
	log(string.Format("VGR_ToolbarItemClicked, run by index: [{0}]", e.Index));
	tb.Visibility = Visibility.Collapsed;
	draw.IsEnabled = true;
	switch(e.Index) {
		case 0: // point
			draw.DrawMode = DrawMode.Point;
			markType = "Флажок";
			break;
		case 1: // line
			draw.DrawMode = DrawMode.Polyline;
			markType = "Полилиния";
			break;
		case 2: // area
			draw.DrawMode = DrawMode.Polygon;
			markType = "Полигон";
			break;
		case 3: // textsymbol
			draw.DrawMode = DrawMode.Point;
			markType = "Текст";
			break;
		default: // close tool
			draw.DrawMode = DrawMode.None;
			draw.IsEnabled = false;
			markType = "";
			break;
	} // end switch
}

private void VGR_ToolbarIndexChanged(object sender, ESRI.ArcGIS.Client.Toolkit.SelectedToolbarItemArgs e) {
	//StatusTextBlock.Text = e.Item.Text;
	log(string.Format("VGR_ToolbarIndexChanged, selected type: [{0}]", e.Item.Text));
}
```

Have fun!

License
-------

[Microsoft Public License (Ms-PL)](http://esrisilverlight.codeplex.com/license)

Links
-----

* http://vasnake.blogspot.com/2012/11/toolbar.html
* https://www.arcgis.com/home/item.html?id=d0d90aae25604cdca900791589b4856a
* https://geonet.esri.com/search.jspa?q=ESRI.ArcGIS.Client.Toolkit.Toolbar
* http://esrisilverlight.codeplex.com/releases/view/60154
* http://www.allgis.org/cartobonus/help/
