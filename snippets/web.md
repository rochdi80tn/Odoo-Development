---
prev: ./snippets.md
---
# Web
## Address Layout  
### Format Address Block  
ID: `mint_system.web.address_layout.format_address_block`  
```xml
<?xml version="1.0"?>
<data inherit_id="web.address_layout" priority="50">

  <xpath expr="//t[@t-if='address']" position="replace">
    <t t-if="address">
      <div class="address row">
        <t t-if="information_block">
          <t t-set="colclass" t-value="'col-5 offset-1'"/>
          <div name="information_block" class="col-5 offset-1">
            <t t-raw="information_block"/>
          </div>
        </t>
      </div>
      <div class="row">
        <div name="address" t-att-class="'col-5 offset-1'">
          <t t-raw="address"/>
        </div>
      </div>
    </t>

  </xpath>

</data>

```
Source: [snippets/web.address_layout.format_address_block.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.address_layout.format_address_block.xml)

### Repositioning Address Blocks  
ID: `mint_system.web.address_layout.repositioning_address_blocks`  
```xml
<?xml version="1.0"?>
<data inherit_id="web.address_layout" priority="50">

    <xpath expr="//t[@t-if='address']" position="replace">

        <t t-if="address">
            <div class="address row">
                <t t-if="address">
                    <t t-set="colclass" t-value="'col-5 offset-1'" />
                    <div name="address" class="col-6">
                        <t t-raw="address" />
                    </div>
                </t>
                <div name="information_block" t-att-class="colclass">
                    <t t-raw="information_block" />
                </div>
            </div>
        </t>

    </xpath>

</data>
```
Source: [snippets/web.address_layout.repositioning_address_blocks.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.address_layout.repositioning_address_blocks.xml)

## Assets Common  
### Pivot Measure White Space  
ID: `mint_system.web.assets_common.pivot_measure_white_space`  
```xml
<?xml version="1.0"?>
<data inherit_id="web.assets_common" priority="50">

    <xpath expr="." position="inside">        
        <style>
            .o_pivot table thead th:not(.o_pivot_header_cell_closed):not(.o_pivot_header_cell_opened):not(.o_pivot_header_cell) {
              white-space: pre-wrap;
            }
        </style>
    </xpath>

</data>

```
Source: [snippets/web.assets_common.pivot_measure_white_space.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.assets_common.pivot_measure_white_space.xml)

### Set Chatter Width  
ID: `mint_system.web.assets_common.set_chatter_width`  
```xml
<?xml version="1.0"?>
<data inherit_id="web.assets_common" priority="50">

    <xpath expr="." position="inside">
        <style>
          @media (min-width: 1534px) {
            .o_FormRenderer_chatterContainer {
              max-width: 600px !important;
            }
          }
        </style>
    </xpath>

</data>
```
Source: [snippets/web.assets_common.set_chatter_width.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.assets_common.set_chatter_width.xml)

### Set Form Width  
ID: `mint_system.web.assets_common.set_form_width`  
```xml
<?xml version="1.0"?>
<data inherit_id="web.assets_common" priority="50">

  <xpath expr="." position="inside">
    <style>
          @media (min-width: 992px) {
          .o_form_view .o_form_sheet_bg > .o_form_sheet {
               max-width: 1450px !important;
            }
          }
    </style>
  </xpath>

</data>
```
Source: [snippets/web.assets_common.set_form_width.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.assets_common.set_form_width.xml)

## Brand Promotion Message  
### Remove  
ID: `mint_system.web.brand_promotion_message.remove`  
```xml
<?xml version="1.0"?>
<data inherit_id="web.brand_promotion_message" priority="50">

  <xpath expr="//t[@name='Brand Promotion Message']" position="replace">
  	<t name="Brand Promotion Message" t-name="web.brand_promotion_message"></t>
  </xpath>

</data>

```
Source: [snippets/web.brand_promotion_message.remove.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.brand_promotion_message.remove.xml)

## External Layout Boxed  
### Footer Company Registry  
ID: `mint_system.web.external_layout_boxed.footer_company_registry`  
```xml
<?xml version="1.0"?>
<data inherit_id="web.external_layout_boxed" priority="50">

  <xpath expr="//li[@t-if='company.vat']" position="after">
    <t t-if="company._name != 'base.document.layout'">
      <li t-if="company.company_registry" class="list-inline-item d-inline">CRN: <span t-field="company.company_registry"/>
      </li>
    </t>
  </xpath>

</data>

```
Source: [snippets/web.external_layout_boxed.footer_company_registry.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.external_layout_boxed.footer_company_registry.xml)

## External Layout Standard  
### Eksb Layout  
ID: `mint_system.web.external_layout_standard.eksb_layout`  
```xml
<?xml version="1.0"?>
<data inherit_id="web.external_layout_standard" priority="50">

  <xpath expr="/t/div" position="replace">
    <div t-attf-class="header o_company_#{company.id}_layout" t-att-style="report_header_style">
      <div class="row">
        <div class="col-3">
          <img t-if="company.logo" t-att-src="image_data_uri(company.logo)" style="max-height: 150px;" alt="Logo"/>
        </div>
        <div class="col-9" name="company_address">
          <style>
            #header-info {
                border-top: black 3px solid;
                border-bottom: black 3px solid;
                font-size: 0.9rem;
                margin-right: 15px;
            }
            div.company {
              word-wrap: normal;
              text-transform: uppercase;
            }
          </style>
          <div class="row" style="height: 50px">
          </div>
          <div id="header-info" class="row">
            <div class="col-3 company">
              <span class="o_bold">Kleinbrauerei<br/>Stiär Biär AG</span>
            </div>
            <div class="col-1"/>
            <div class="col-4">
              <span t-field="company.partner_id.street"/>
              <br/>
              <span t-field="company.partner_id.zip"/>
              <span t-field="company.partner_id.city"/>
            </div>
            <div class="col-4">
              <span t-field="company.partner_id.phone"/>
              <br/>
              <span t-field="company.partner_id.email"/>
            </div>
          </div>
        </div>
      </div>
    </div>
  </xpath>

</data>

```
Source: [snippets/web.external_layout_standard.eksb_layout.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.external_layout_standard.eksb_layout.xml)

### Footer Company Registry  
ID: `mint_system.web.external_layout_standard.footer_company_registry`  
```xml
<?xml version="1.0"?>
<data inherit_id="web.external_layout_standard" priority="50">

  <xpath expr="//li[@t-if='company.vat']" position="after">
    <t t-if="company._name != 'base.document.layout'">
      <li t-if="company.company_registry" class="list-inline-item d-inline">CRN: <span t-field="company.company_registry"/>
      </li>
    </t>
  </xpath>

</data>

```
Source: [snippets/web.external_layout_standard.footer_company_registry.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.external_layout_standard.footer_company_registry.xml)

### Format Header Slogan  
ID: `mint_system.web.external_layout_standard.format_header_slogan`  
```xml
<?xml version="1.0"?>
<data inherit_id="web.external_layout_standard" priority="50">

  <xpath expr="//div[@name='moto']" position="replace">
    <style>
      h4 {
        /* align-self: center; */
        padding-top: 2rem;
      }
    </style>
    <h4 class="col-9 text-right" t-field="company.report_header" name="moto"/>
  </xpath>

</data>
```
Source: [snippets/web.external_layout_standard.format_header_slogan.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.external_layout_standard.format_header_slogan.xml)

### Header Styles  
ID: `mint_system.web.external_layout_standard.header_styles`  
```xml
<?xml version="1.0"?>
<data inherit_id="web.external_layout_standard" priority="50">

  <xpath expr="/t/div" position="before">
    <style>
	    h2 {
	      font-size: 18px;
	    }	                          
    </style>

  </xpath>
</data>
```
Source: [snippets/web.external_layout_standard.header_styles.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.external_layout_standard.header_styles.xml)

### Increase Logo Size  
ID: `mint_system.web.external_layout_standard.increase_logo_size`  
```xml
<?xml version="1.0"?>
<data inherit_id="web.external_layout_standard" priority="50">

  <xpath expr="//img[@t-if='company.logo']" position="attributes">
    <attribute name="style">max-height: 90px;</attribute>
  </xpath>

</data>

```
Source: [snippets/web.external_layout_standard.increase_logo_size.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.external_layout_standard.increase_logo_size.xml)

### Remove Company Info Footer  
ID: `mint_system.web.external_layout_standard.remove_company_info_footer`  
```xml
<?xml version="1.0"?>
<data inherit_id="web.external_layout_standard" priority="50">

  <xpath expr="//div[@name='financial_infos']/../ul[1]" position="replace">
  </xpath>

</data>

```
Source: [snippets/web.external_layout_standard.remove_company_info_footer.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.external_layout_standard.remove_company_info_footer.xml)

### Remove Contact  
ID: `mint_system.web.external_layout_standard.remove_contact`  
```xml
<?xml version="1.0"?>
<!-- Remove contact info in footer -->
<data inherit_id="web.external_layout_standard" priority="50">

  <!-- Works until Odoo 14.0 -->
	<xpath expr="//li[@t-if='company.phone']" position="replace">
  </xpath>
  <xpath expr="//li[@t-if='company.email']" position="replace">
  </xpath>

</data>

```
Source: [snippets/web.external_layout_standard.remove_contact.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.external_layout_standard.remove_contact.xml)

### Remove Header Address  
ID: `mint_system.web.external_layout_standard.remove_header_address`  
```xml
<?xml version="1.0"?>
<data inherit_id="web.external_layout_standard" priority="50">

  <xpath expr="//div[@name='company_address']" position="replace">
  </xpath>

</data>

```
Source: [snippets/web.external_layout_standard.remove_header_address.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.external_layout_standard.remove_header_address.xml)

### Replace Footer  
ID: `mint_system.web.external_layout_standard.replace_footer`  
```xml
<?xml version="1.0"?>
<data inherit_id="web.external_layout_standard" priority="50">

  <xpath expr="/t/div[3]" position="replace">
    <div t-attf-class="footer o_standard_footer o_company_#{company.id}_layout">
     <div align="right" style="color:black; font-size:9pt">
         Page: <span class="page"/> / <span class="topage"/>
     </div>
     </div>
  </xpath>

</data>
```
Source: [snippets/web.external_layout_standard.replace_footer.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.external_layout_standard.replace_footer.xml)

### Replace Header  
ID: `mint_system.web.external_layout_standard.replace_header`  
```xml
<?xml version="1.0"?>
<data inherit_id="web.external_layout_standard" priority="50">

<xpath expr="/t/div" position="replace">    
  <div t-attf-class="header o_company_#{company.id}_layout" t-att-style="report_header_style">
                           
<table style="width:100%; font-size: 9pt; color:rgb(102,102,102); font-family:arial;">
  
  <tr height="27px;">
    <td style="width:19%; border-left: 1px solid rgb(102,102,102);"></td>
    <td style="width:18%; border-left: 1px solid rgb(102,102,102);"></td>
    <td style="width:25%; border-left: 1px solid rgb(102,102,102);"></td>
    <td style="width:38%; margin: 0; vertical-align:bottom; padding:0;" rowspan="4"><img t-if="company.logo" t-att-src="image_data_uri(company.logo)" alt="Logo"  style="height:61px; float:right"/></td>
  </tr>
 
  <tr style="line-height: 1.2;">
    <td style="border-left: 1px solid rgb(102,102,102); padding-left: 10px;"><span t-field="company.name"/></td>
    <td style="border-left: 1px solid rgb(102,102,102);"></td>
    <td style="border-left: 1px solid rgb(102,102,102);"></td>
  </tr>
  <tr style="line-height: 1.2;">
    <td style="border-left: 1px solid rgb(102,102,102); padding-left: 10px;"><span t-field="company.partner_id.street"/></td>
    <td style="border-left: 1px solid rgb(102,102,102); padding-left: 10px;">Tel. 056 618 77 00</td>
    <td style="border-left: 1px solid rgb(102,102,102); padding-left: 10px;">www.trimada.ch</td>
  </tr>
  <tr style="line-height: 1.2;">
    <td style="border-left: 1px solid rgb(102,102,102); padding-left: 10px;">CH-<span t-field="company.partner_id.zip"/> <span t-field="company.partner_id.city"/></td>
    <td style="border-left: 1px solid rgb(102,102,102); padding-left: 10px;">Fax 056 618 77 07</td>
    <td style="border-left: 1px solid rgb(102,102,102); padding-left: 10px;"><span t-field="company.partner_id.email"/></td>
  </tr>
 
</table>


  </div>
</xpath>
</data>
```
Source: [snippets/web.external_layout_standard.replace_header.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.external_layout_standard.replace_header.xml)

### Replace Url  
ID: `mint_system.web.external_layout_standard.replace_url`  
```xml
<?xml version="1.0"?>
<!-- Replace website url in document footer -->
<data inherit_id="web.external_layout_standard" priority="50">

  <!-- Works until Odoo 14.0 -->
  <xpath expr="//li[@t-if='company.website']" position="replace">
  	<li t-if="company.website" class="list-inline-item d-inline">www.example.ch</li>
  </xpath>

</data>

```
Source: [snippets/web.external_layout_standard.replace_url.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.external_layout_standard.replace_url.xml)

## Internal Layout  
### Header Styles  
ID: `mint_system.web.internal_layout.header_styles`  
```xml
<?xml version="1.0"?>
<data inherit_id="web.internal_layout" priority="50">

  <xpath expr="/t/div" position="before">
    <style>
	    h2 {
	      font-size: 18px;
	    }	                          
    </style>

  </xpath>
</data>
```
Source: [snippets/web.internal_layout.header_styles.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.internal_layout.header_styles.xml)

### Replace Header  
ID: `mint_system.web.internal_layout.replace_header`  
```xml
<?xml version="1.0"?>
<data inherit_id="web.internal_layout" priority="50">

	<xpath expr="//div[@class='header']" position="replace">
		<div class="header">
			<div class="row">
				<div class="col-4">
				</div>
				<div class="col-4 text-center">
				</div>
				<div class="col-4 text-right">
					<img t-if="company.logo" t-att-src="image_data_uri(company.logo)" alt="Logo" style="height:61px; margin-right: 40px;"/>
				</div>
			</div>
		</div>
	</xpath>

</data>
```
Source: [snippets/web.internal_layout.replace_header.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.internal_layout.replace_header.xml)

## Styles Company Report  
### Set Font  
ID: `mint_system.web.styles_company_report.set_font`  
```xml
<?xml version="1.0"?>
<data inherit_id="web.styles_company_report" priority="50">

  <xpath expr="//t[@t-set='font']" position="replace">
    <t t-set="font" t-value="'arial'"/>
  </xpath>

</data>
```
Source: [snippets/web.styles_company_report.set_font.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/web.styles_company_report.set_font.xml)

