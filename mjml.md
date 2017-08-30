![](https://mjml.io/assets/img/logo-small.png)


```
shell> npm install mjml
shell> npm i -g mjml
shell> ./node_modules/.bin/mjml index.mjml
shell> mjml input.mjml -o my-email.html
```
```
shell> mjml -r index.mjml
shell> mjml -r index.mjml -o index.html
shell> mjml --watch index.mjml index.html
```

```
<mjml>
  <mj-body>
    <mj-container>
      <mj-section>
        <mj-column>

          <mj-image width="100" src="/assets/img/logo-small.png"></mj-image>

          <mj-divider border-color="#F45E43"></mj-divider>

          <mj-text font-size="20px" color="#F45E43" font-family="helvetica">Hello World</mj-text>

        </mj-column>
      </mj-section>
    </mj-container>
  </mj-body>
</mjml>
```


```
<mjml>
  <mj-body>
    <mj-container>
      <mj-section>
        <mj-column>
          <mj-text>Hi sexy!</mj-text>
        </mj-column>
      </mj-section>
    </mj-container>
  </mj-body>
</mjml>
```

```
<mjml>
  <mj-body>
    <mj-container>

      <!-- Company Header -->
      <mj-section background-color="#f0f0f0"></mj-section>

      <!-- Image Header -->
      <mj-section background-color="#f0f0f0"></mj-section>

      <!-- Introduction Text -->
      <mj-section background-color="#fafafa"></mj-section>

      <!-- 2 columns section -->
      <mj-section background-color="white"></mj-section>

      <!-- Icons -->
      <mj-section background-color="#fbfbfb"></mj-section>

      <!-- Social icons -->
      <mj-section background-color="#f0f0f0"></mj-section>

    </mj-container>
  </mj-body>
</mjml>
```

`mj-head`
```
<mj-head>
</mj-head>

<mj-font name="Raleway" href="https://fonts.googleapis.com/css?family=Raleway" />
<mj-title>Hello MJML</mj-title>

<mj-attributes>
  <mj-text padding="0" />
  <mj-class name="blue" color="blue" />
  <mj-class name="big" font-size="20px" />
  <mj-all font-family="Arial" />
</mj-attributes>

```

```
<mj-container>
</mj-container>

<mj-container background-color="#E1E8ED">
</mj-container>

<mj-wrapper full-width="full-width" background-color="red">
  <!-- Your sectios go here -->
</mj-wrapper>

<mj-section background-color="#fafafa">
</mj-section>

<mj-section background-color="white">
</mj-section>

<mj-section padding-bottom="0" background-color="#f3f3f3">
</mj-section>

<mj-section background-color="#fcfcfc" padding-top="20px">
</mj-section>

<mj-column width="400">
</mj-column>

<mj-image width="100" src="/assets/img/logo-small.png"></mj-image>
<mj-image src="https://mjml.io/assets/img/easy-and-quick.png" width="100" />
<mj-image width="300" src="http://www.online-image-editor.com//styles/2014/images/example_image.png" />

<mj-divider border-width="1px" border-style="dashed" border-color="lightgrey" />
<mj-divider border-width="1px" border-style="solid" border-color="lightgrey" />
<mj-divider border-color="#F45E43"></mj-divider>
<mj-divider
    padding-top="20"
    padding-bottom="0"
    padding-left="0"
    padding-right="0"
    border-width="1px"
    border-color="#f8f8f8"/>
<mj-divider 
    border-color="#ffffff"
    border-width="2px"
    border-style="solid"
    vertical-align="middle"
    padding-left="20"
    padding-right="20"
    padding-bottom="0"
    padding-top="0">
</mj-divider>

<mj-text font-size="20px" color="#F45E43" font-family="helvetica">Hello World</mj-text>
<mj-text font-style="italic" font-size="20" font-family="Helvetica Neue" color="#626262">My Awesome Text</mj-text>
<mj-text align="center">Hello World</mj-text>
<mj-text color="#525252">
  Hello World!
</mj-text>

<mj-text font-size="20px" color="#F45e46" font-family="helvetica">
  Hello <a href="https://mjml.io" class="link-nostyle">World</a>
</mj-text>

<mj-text align="center" font-size="20" color="rgb(165, 176, 184)">
  Hello World!
</mj-text>

<mj-text align="left" font-size="20" color="grey">
  Hello World
</mj-text>

<mj-text mj-class="blue big">
  Hello World!
</mj-text>

<mj-text font-family="Raleway, Arial">
  Hello World!
</mj-text>

<mj-social mode="vertical" display="twitter facebook" />
<mj-social
  mode="vertical"
  display="google facebook"
  google-icon-color="#424242"
  facebook-icon-color="#424242"
  facebook-href="My facebook page"
  google-href="My google+ page" />

<mj-button background-color="#F45E43" href="#">Hello World</mj-button>

<mj-button font-family="Helvetica" background-color="#f45e43" color="white">
  Don't click me!
</mj-button>

<mj-spacer height="50px" />

<mj-table>
  <tr style="border-bottom:1px solid #ecedee;text-align:left;padding:15px 0;">
    <th style="padding: 0 15px 0 0;">Year</th>
    <th style="padding: 0 15px;">Language</th>
    <th style="padding: 0 0 0 15px;">Inspired from</th>
  </tr>
  <tr>
    <td style="padding: 0 15px 0 0;">1995</td>
    <td style="padding: 0 15px;">PHP</td>
    <td style="padding: 0 0 0 15px;">C, Shell Unix</td>
  </tr>
  <tr>
    <td style="padding: 0 15px 0 0;">1995</td>
    <td style="padding: 0 15px;">JavaScript</td>
    <td style="padding: 0 0 0 15px;">Scheme, Self</td>
  </tr>
</mj-table>


<mj-carousel>
  <mj-carousel-image src="https://www.mailjet.com/wp-content/uploads/2016/11/ecommerce-guide.jpg" />
  <mj-carousel-image src="https://www.mailjet.com/wp-content/uploads/2016/09/3@1x.png" />
  <mj-carousel-image src="https://www.mailjet.com/wp-content/uploads/2016/09/1@1x.png" />
</mj-carousel>

```


```
      <!-- Intro text -->
      <mj-section background-color="#fafafa">
        <mj-column width="400">

          <mj-text font-style="italic" font-size="20" font-family="Helvetica Neue" color="#626262">My Awesome Text</mj-text>

          <mj-text color="#525252">
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin rutrum enim eget magna efficitur, eu semper augue semper. Aliquam erat volutpat. Cras id dui lectus. Vestibulum sed finibus lectus, sit amet suscipit nibh. Proin nec commodo purus. Sed eget
            nulla elit. Nulla aliquet mollis faucibus.
          </mj-text>

          <mj-button background-color="#F45E43" href="#">Learn more</mj-button>

        </mj-column>
      </mj-section>
```


```
 <mjml>
   <mj-head>
     <mj-font name="Raleway" href="https://fonts.googleapis.com/css?family=Raleway" />
   </mj-head>
   <mj-body>
     <mj-container>
       <mj-section>
         <mj-column>
           <mj-text font-family="Raleway, Arial">
             Hello World!
           </mj-text>
         </mj-column>
       </mj-section>
     </mj-container>
   </mj-body>
 </mjml>
```

- https://mjml.io/try-it-live/templates/basic


---
```
const mjml2html = require('mjml');
const htmlOutput = mjml2html(`
  <mjml>
    <mj-body>
      <mj-container>
        <mj-section>
          <mj-column>
            <mj-text>
              Hello World!
            </mj-text>
          </mj-column>
        </mj-section>
      </mj-container>
    </mj-body>
  </mjml>
`)
console.log(htmlOutput)
```

#### :books: 參考網站：
- [Documentation](https://mjml.io/documentation)
- [Try it live](https://mjml.io/try-it-live)
- https://mjml.io/try-it-live/components/head-attributes
- https://mjml.io/templates
