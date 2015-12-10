If Item is heightless, it will not be positioned inside Column and other Items could not depend on its real bottom.
ListView is heightless, for example, even if it has some visible content.

`height` (Item) — basic height
`implicitHeight` (Item) — height based on the content (Image, Text)
`contentHeight` (Flickable) — height of the content ( == `contentItem.childrenRect.height`)
