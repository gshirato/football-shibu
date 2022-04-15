# FOOTBALL-SHIBU
- Make XML for podcast feed
- file: https://raw.githubusercontent.com/gshirato/concast/main/football-shiv-feed.xml
## Apple Podcast RSS feed requirements
See [requirements in general](https://podcasters.apple.com/support/823-podcast-requirements).
See [requirements of tags](https://help.apple.com/itc/podcasts_connect/#/itcb54353390)

> When you use tags specific to Apple Podcasts, indicated by a leading <itunes:> prefix, you must add the following namespace declaration as the second line in your XML:

```xml
<rss xmlns:itunes="http://www.itunes.com/dtds/podcast-1.0.dtd" version="2.0">
```

### Channel Tags

#### Required Tags
- `<channel>`
    - `<title>`
    - `<description>`
    - `<itunes:image>`
    - `<language>`
    - `<itunes:category>`
    - `<itunes:explicit>`

#### Recommended tags
- `<channel>`
    - `<itunes:author>`
    - `<link>`
    - `<itunes:owner>`
    - `<language>`
#### Situational tags
- `<channel>`
    - `<itunes:title>`
    - `<itunes:type>`
    - `<copyright>`
    - `<itunes:new-feed-url>`
    - `<itunes:block>`
    - `<itunes:complete>`

### Episode tags

#### Required Tags
- `<item>`
    - `<enclosure>`

#### Recommended tags
- `<item>`
    - `<guid>`
    - `<pubDate>`
    - `<description>`
    - `<itunes:duration>`
    - `<link>`
    - `<itunes:image>`
    - `<itunes:explicit>`

#### Situational tags
- `<item>`
    - `<itunes:title>`
    - `<itunes:episode>`
    - `<itunes:season>`
    - `<itunes:episodeType>`
    - `<itunes:block>`


## Heads-up when making an RSS file

We use `from xml.etree import ElementTree as ET`.

### Namespace
Namespace should be specified.
```python
rss_attrs = {
    'version':'2.0',
    'xmlns:itunes': 'http://www.itunes.com/dtds/podcast-1.0.dtd',
    'xmlns:content': 'http://purl.org/rss/1.0/modules/content/'
}
```

Without this, we would get `ParseError: unbound prefix`.

### Options
To write an XML file, the `ET.ElementTree` object should be first converted into `string` with options `encoding='unicode'` and `xml_declaration=True`. Then, the string object is parsed with `xml.dom.minidom.parseString`.

```python
document = xml.dom.minidom.parseString(ET.tostring(dom, 'unicode', xml_declaration=True))
with open('feed.xml', 'w') as f:
    document.writexml(f, encoding='unicode', newl='\n', indent='', addindent='\t')
```
