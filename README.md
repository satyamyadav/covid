## COVID-19 Tracker App
Welcome! This tutorial will guide you in creating an awesome app with the Innovaccer Design System. Here is a [preview](https://covid19-tracker.info/) of the app that we are going to build.

**Audience**
This tutorial is intended for people with all amounts of web development experience. If you want to jump straight to code, you may want to skip this tutorial and go to the [developer guidelines](https://github.com/aregee/design-system/blob/master/README.md) page.

**Getting Started**
Each step in this guideline illustrates a different aspect of developing web applications with Innovaccer design system. Refer the following sections below to get familiar with this project:
* [Installation](#Installation)
* [Building Landing Page](#BUILDING_LANDING_PAGE)


### <a name="Installation"></a>Installation
We will start with `Create React App`.
```
npx create-react-app covid
cd covid
npm start
```
Next, you need to install Innovaccer design system in your project. You need to follow the [developer guidelines](https://github.com/aregee/design-system/blob/master/README.md) steps to install the design system.

### <a name="#BUILDING_LANDING_PAGE"></a>Building Landing Page
A preview of what you will build:
![Covid App]()

Lets begin by creating a React component called Home. In the src directory, create a Home directory. Create the following files inside *src/Home/index.js* and *src/Home/Home.css*:
```
src/Home
├──index.js
├──Home.css
```
##### Add landing page grid
We will break our landing page into two rows. The first row looks like it has two columns of different widths and the second row has two columns of equal width. Now that we’re building the page with grid, we need to import grid from our *design-system* package to *Home/index.js*.
```
import { Row, Column } from 'design-system';
```
We can continue to make rows by adding a *<Row>*, as well as make columns within those rows by adding *<Column>*. Column sizes are specified by the number of columns they’ll be spanning. If we add props like *size={12}* , it means it’ll span 12 columns. If we add *sizeXL={7}*, it’ll span 7 columns when screen size is large, and so on. So, for our landing page, we will two make rows in *Home/index.js* like:
```
<div>
    <Row>
        <Column size={12} sizeXL={7}>...</Column>
        <Column size={12} sizeXL={5}>...</Column>
    </Row>
    <Row>
        <Column size={6} sizeM={12} sizeXS={12}>...</Column>
        <Column size={6} sizeM={12} sizeXS={12}>...</Column>
    </Row>
</div>
```
Now, to maintain modularity, we can further divide the columns into components.
In the src directory, create Map, CovidInfo and Summary.

##### First Row
In our first row, we will have two components Map and CovidInfo. Each component represents a column. First, for the `Map component` let’s import the components we need. Because we’ll be importing several components for this page, we’ll import them directly from the *design-system* package instead of the direct path for each one. In our *Maps/index.js*, we need to add:
```
import { Heading, Subheading, Card } from 'design-system';
```
We want to wrap the map inside a card. For this, we will be using the Card Component.
```
<Card
    shadow="light"
    style={{
        backgroundColor: 'white'
    }}
>
    <ChoroplethMap
        statistic={statistic}
        mapData={currentMapData}
        changeMap={switchMapToState}
        selectedRegion={selectedRegion}
        setSelectedRegion={setSelectedRegion}
        isCountryLoaded={isCountryLoaded}
     />
</Card>
```
Now, we can add Heading and Subheading components like:
```
<Heading size="m"> Map </Heading>
<Subheading appearance="subtle" size="s">
    Hover for more details
</Subheading>
```
Moving on to `CovidInfo component`, we can follow the similar steps in *CovidInfo/index.js*
```
import { Card, Text, Heading } from 'design-system';
```
We can wrap the information in Card and add text in the following way:
```
 <Card>
    <Heading>Precautions</Heading>
    <Text>Use a medical face mask</Text>
</Card>
```
##### Second Row
In our second row, we will move on to `Summary component`. We can add a *Card* and *Heading* by following the same steps as we did for the first row. Now, we need to add *Legend* and *DonutChart* and *Icon* in *Summary/index.js* :
```
import { Card, Heading, Subheading, Legend, Icon, DonutChart } from 'design-system';
```
We can add icon in the following way:
```
<div className="Summary-heading">
    <Heading size="m">India Statistics</Heading>
    <Icon name="open_in_new" appearance="subtle" size="24" onClick={() => handleMore(entity)} />
</div>
```
To add Donut Chart and Legend:
```
<Column>
    <div className="Summary-details">
        <Legend labelWeight="medium" iconAppearance="primary" label="Active" />
        <Legend labelWeight="medium" iconAppearance="alert" label="Deaths" />
    </div>
</Column>
<Column>
    <DonutChart
        data={data}
        withCenterText={false}
        withActiveSegment={!isMobile}
        withTooltip={isMobile}
        donutWidth={60}
        colors={['primary', 'success', 'alert']}
    />
</Column>
```
### Building Drilled Page





