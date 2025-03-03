---
prev: ./snippets.md
---
# Sale
## Report Blanketorder Document  
### Add Drawing  
ID: `mint_system.sale.report_blanketorder_document.add_drawing`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_blanketorder_document" priority="50">
 
<xpath expr="//span[@t-field='l.name']" position="after">
  <br/>
  <span>Drawing: </span>
    <a t-attf-href="{{l.product_id.drawing_file.url}}">
    <span t-field="l.product_id.drawing_file.display_name"/>
    </a>
</xpath>

</data>
```
Source: [snippets/sale.report_blanketorder_document.add_drawing.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_blanketorder_document.add_drawing.xml)

### Add Footer  
ID: `mint_system.sale.report_blanketorder_document.add_footer`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_blanketorder_document" priority="50">

<xpath expr="//p[@t-if='doc.payment_term_id.note']" position="replace">
  <style>
      table#footer {
        width: 100%;
        font-size: 8pt;
      }
      table#footer tr, td {
        vertical-align: top;
      }
    </style>
    <table id='footer'>
      <tr>
        <td width="40%" t-if="doc.payment_term_id.note">Zahlungsbedingungen 
          <span t-field="doc.payment_term_id.note"/>
        </td>
        <td width="60%">
          Lieferung gemäss unseren allgemeinen Lieferbedingungen
        </td>
      </tr>
      <tr>
        <td >MWST-Nr: 
           <span t-field="doc.company_id.vat"/>
        </td>
        <td>
          <table width="100%">
          <tr>
            <td width="35%">
               Bankverbindungen:
            </td>
              <td width="65%">
              UBS AG, 6301 Zug, BLZ 273, SWIFT UBSWCHZH80A
             </td>
          </tr> 
          <tr> 
             <td>
            </td>
            <td>
            (CHF) IBAN CH63 0027 3273 Q978 6962 0
            </td>
          </tr>
       
          <tr>
            <td>
            </td>
            <td>
            (EUR) IBAN CH59 0027 3273 HN10 3698 0
            </td>
          </tr>
          </table> 
        </td>
      </tr>
    </table>
  </xpath>

</data>
```
Source: [snippets/sale.report_blanketorder_document.add_footer.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_blanketorder_document.add_footer.xml)

### Add Infotable  
ID: `mint_system.sale.report_blanketorder_document.add_infotable`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_blanketorder_document" priority="50">

  <xpath expr="//h2" position="after">
    <style>
      table#info {
        width: 100%;
        margin-bottom: 25px;
        font-size: 9pt;
      }
        table#info tr {
        line-height: 1.2;
        text-align: left;
      }
        .note {
        font-size: 9pt;
      }
    </style>
    <table id='info'>
      <tr>
        <td width="17%">Datum Angebot</td>
        <td width="44%">
          <span t-field='doc.date_confirmed' t-options='{ "widget": "date" }'/>
        </td>
        <td width="14%"></td>
        <td width="25%"></td>
      </tr>
      <tr>
        <td>Kunden-Nr.</td>
        <td>
          <span t-field='doc.partner_id.ref'/>
        </td>
        <td>U/Referenz</td>
        <td>
          <span t-field='doc.user_id'/>
        </td>
      </tr>
      <tr>
        <td>I/Referenz</td>
        <td>
          <span t-field='doc.client_order_ref'/>
        </td>
        <td>Versandart</td>
        <td>
          <span t-field='doc.carrier_id'/>
        </td>
      </tr>
      <tr>
        <td>Betreff</td>
        <td>
          <span t-field='doc.comment'/>
        </td>
        <td>Lieferkondition</td>
        <td>
          <span t-field='doc.incoterm'/>
        </td>
      </tr>
    </table>

    <t t-if="doc.note_header != '&lt;p&gt;&lt;br&gt;&lt;/p&gt;'">
      <span class="note" t-field="doc.note_header"/>
    </t>

  </xpath>

</data>
```
Source: [snippets/sale.report_blanketorder_document.add_infotable.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_blanketorder_document.add_infotable.xml)

### Add Payment Terms  
ID: `mint_system.sale.report_blanketorder_document.add_payment_terms`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_blanketorder_document" priority="50">

<xpath expr="/t/t/div/div[3]" position="after">
    <div class="row" style="margin-top: 1rem; margin-bottom: 1rem">
      <div class="col">
         <span>Payment Terms: </span>
         <span t-field="doc.payment_term_id.name"/>
      </div>
    </div>
</xpath>

</data>

```
Source: [snippets/sale.report_blanketorder_document.add_payment_terms.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_blanketorder_document.add_payment_terms.xml)

### Change Column Order  
ID: `mint_system.sale.report_blanketorder_document.change_column_order`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_blanketorder_document" priority="50">
  
<xpath expr="//table[@class='table table-condensed']/thead/tr" position="replace">
    <tr>
        <th>Product</th>
        <th class="text-right">Original Qty</th>
        <th class="text-center">Scheduled Date</th>
        <th class="text-right">Unit Price</th>
        <th class="text-right">Amount</th>
    </tr>
</xpath>
  
<xpath expr="//tbody[@class='sale_tbody']/t" position="replace">
    <t t-foreach="doc.line_ids" t-as="l">
        <tr>
            <td>
                <span t-field="l.name"/>
            </td>
            <td class="text-right">
                <span t-field="l.original_uom_qty"/>
                <span t-field="l.product_uom" groups="uom.group_uom"/>
            </td>
            <td class="text-center">
                <span t-field="l.date_schedule"/>
            </td>
                                
            <td class="text-right">
                <span t-field="l.price_unit"/>
            </td>
            <td class="text-right">
                 <span t-field="l.price_subtotal" t-options="{&quot;widget&quot;: &quot;monetary&quot;, &quot;display_currency&quot;: l.currency_id}"/>
            </td>
        </tr>
     </t>
</xpath>

</data>
```
Source: [snippets/sale.report_blanketorder_document.change_column_order.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_blanketorder_document.change_column_order.xml)

### Change Font  
ID: `mint_system.sale.report_blanketorder_document.change_font`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_blanketorder_document" priority="50">

<xpath expr="//table[@class='table table-condensed']" position="attributes">
     <attribute name="style" add="font-size:16px"/>
  </xpath>

  <xpath expr="//div[@class='col-xs-4 pull-right']" position="attributes">
     <attribute name="style" add="font-size:16px"/>
  </xpath>

</data>

```
Source: [snippets/sale.report_blanketorder_document.change_font.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_blanketorder_document.change_font.xml)

### Format Address Blocks  
ID: `mint_system.sale.report_blanketorder_document.format_address_blocks`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_blanketorder_document" priority="50">

  <xpath expr="//div[@class='col-xs-6']/.." position="replace">
    <t t-set="doc" t-value="doc.with_context({'lang':doc.partner_id.lang})"/>
    <t t-set="address">
      <div t-field="doc.partner_id" t-options="{&quot;widget&quot;: &quot;contact&quot;, &quot;fields&quot;: [&quot;address&quot;, &quot;name&quot;], &quot;no_marker&quot;: True}" style="font-size:10pt; line-height: 1.2; padding-bottom:33mm"/>
      <p t-if="doc.partner_id.vat">
      </p>
    </t>
  </xpath>

</data>
```
Source: [snippets/sale.report_blanketorder_document.format_address_blocks.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_blanketorder_document.format_address_blocks.xml)

### Format Qty  
ID: `mint_system.sale.report_blanketorder_document.format_qty`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_blanketorder_document" priority="50">

  <xpath expr="//span[@t-field='l.original_uom_qty']" position="replace">
    <t t-if="l.product_uom.id == 1">
      <span t-field="l.original_uom_qty" t-options="{'widget': 'integer'}"/>
    </t>
    <t t-else="">
      <span t-field="l.original_uom_qty"/>
    </t>
  </xpath>
  
</data>
```
Source: [snippets/sale.report_blanketorder_document.format_qty.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_blanketorder_document.format_qty.xml)

### Format Title  
ID: `mint_system.sale.report_blanketorder_document.format_title`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_blanketorder_document" priority="50">

  <xpath expr="//h2" position="attributes">
    <attribute name="style">color: black; font-size:13pt; font-weight:bold; margin-top:10mm; margin-bottom:3mm</attribute>
  </xpath>
  
</data>
```
Source: [snippets/sale.report_blanketorder_document.format_title.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_blanketorder_document.format_title.xml)

### Modify Main Table  
ID: `mint_system.sale.report_blanketorder_document.modify_main_table`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_blanketorder_document" priority="50">

  <!-- add default_code   -->
  <xpath expr="//table/thead/tr/th[1]" position="after">
    <th>
      <span>Artikel Nr.</span>
    </th>
  </xpath>
  <xpath expr="//table/tbody/t/tr/t[1]/td[1]" position="after">
    <td>
      <span t-field="line.product_id.default_code"/>
    </td>
  </xpath>

  <!-- replace product description -->
  <xpath expr="//table/tbody/t[2]/tr/t[1]/td[3]/span" position="replace">
    <t>
      <span style="font-weight:bold;" t-field="line.product_id.type_description"/>
    </t>
  </xpath>

  <!-- add second row -->
  <xpath expr="//tbody//tr[1]" position="after">
    <tr>
      <td style="padding-bottom :10px; padding-left:3px; line-height: 1.2"></td>
      <td style="padding:0; padding-left:3px; line-height: 1.2"></td>
      <td style="padding:0; padding-left:3px; line-height: 1.2" colspan="4">
        <span t-field="line.name"/>
        <br/>
        <t t-if="line.product_id.country_of_origin_id.code">Ursprungsland: <span t-field="line.product_id.country_of_origin_id.code"/>
        </t>
        <t t-if="line.product_id.hs_code"> / Zollposition: <span t-field="line.product_id.hs_code"/>
        </t>
      </td>
      <td></td>
    </tr>
    <tr style="border-bottom: 1px solid rgb(220,220,220)">
      <td colspan="8"></td>
    </tr>
  </xpath>

  <!-- format main_table -->
  <xpath expr="//table[@class='table table-sm o_main_table']" position="attributes">
    <attribute name="style">width: 100%; font-size:9pt</attribute>
    <attribute name="class">table table-borderless table-sm</attribute>
  </xpath>

  <!-- header-->
  <xpath expr="//table[@class='table table-borderless table-sm']/thead/tr" position="attributes">
    <attribute name="style">border-top:solid 1px; border-bottom: solid 1px; color: black;</attribute>
  </xpath>

  <!-- header: position -->
  <xpath expr="//table[@class='table table-borderless table-sm']/thead/tr/th[1]" position="attributes">
    <attribute name="style">width: 5mm</attribute>/>
  </xpath>

  <!-- header: default code -->
  <xpath expr="//table[@class='table table-borderless table-sm']/thead/tr/th[2]" position="attributes">
    <attribute name="style">width: 27mm; text-align: right; padding-right: 10px</attribute>"/>
  </xpath>

  <!-- header: description -->
  <xpath expr="//table[@class='table table-borderless table-sm']/thead/tr/th[3]" position="attributes">
    <attribute name="style">width: 70mm</attribute>/>
  </xpath>

  <!-- header: qty -->
  <xpath expr="//table[@class='table table-borderless table-sm']/thead/tr/th[5]" position="attributes">
    <attribute name="style">text-align: right; padding-right: 5px</attribute>"/>
    <attribute name="style">width: 30mm</attribute>/>
  </xpath>

  <!-- position -->
  <xpath expr="//table[@class='table table-borderless table-sm']/tbody/t[2]/tr/t[1]/td[1]" position="attributes">
    <attribute name="style">text-align: right</attribute>/>
  </xpath>

  <!-- default code -->
  <xpath expr="//table[@class='table table-borderless table-sm']/tbody/t[2]/tr/t[1]/td[2]" position="attributes">
    <attribute name="style">text-align: right; padding-right: 10px</attribute>/>
  </xpath>

  <!-- commitment date -->
  <xpath expr="//table[@class='table table-borderless table-sm']/tbody/t[2]/tr/t[1]/td[4]" position="attributes">
    <attribute name="style">text-align: left;</attribute>/>
  </xpath>
  
   <!-- qty   -->
  <xpath expr="/t/t/div/table[2]/tbody/t[2]/tr[1]/t[1]/td[5]/span[1]" position="attributes">
    <attribute name="class" separator=" " add="o_bold"/>
     <attribute name="t-options-widget">"integer"</attribute>
  </xpath>

  <!-- price -->
  <xpath expr="//table[@class='table table-borderless table-sm']/tbody/t[2]/tr/t[1]/td[7]/span" position="replace">
    <span t-esc="'%g' % line.price_unit if str(line.price_unit)[::-1].find('.') >= 3 else '%.2f' % line.price_unit"/>
  </xpath>

  <!-- remove taxes -->
  <xpath expr="//thead/tr[1]/th[9]" position="replace"/>
  <xpath expr="//tbody/t[2]/tr[1]/t[1]/td[9]" position="replace"/>

  <!-- margin -->
  <xpath expr="//table[@class='table table-borderless table-sm']/tbody/t[2]/tr/t[1]/td[8]/span" position="replace">
    <span t-field="line.discount"/>%
  </xpath>

  <!-- total price -->
  <xpath expr="//table[@class='table table-borderless table-sm']/tbody[1]/t[2]/tr[1]/t[1]/td[9]/span" position="replace">
    <span t-esc="'{0:,.2f}'.format(int(line.price_subtotal)).replace(',','\'')"/>
  </xpath>

  <xpath expr="//table[@class='table table-borderless table-sm']" position="after">
    <t t-if="doc.note_footer != '&lt;p&gt;&lt;br&gt;&lt;/p&gt;'">
      <span class="note" t-field="doc.note_footer"/>
    </t>
    <table class="table table-borderless table-sm" style="margin-top:20px; width:100%; color:black; font-family: arial; font-size:9pt; border-top-style:solid; border-bottom-style:solid; border-width:1px; border-color:black">
      <t t-foreach="doc.amount_by_group" t-as="amount_by_group">
        <tr >
          <td style="width:15.5%; text-align:left">
            <Strong>Warenwert</Strong>
          </td>
          <td style="width:23%; text-align:left">
            <span t-field="doc.amount_untaxed"/>
          </td>
          <td style="width:12%; text-align:left">
            <span t-esc="amount_by_group[0]"/>
          </td>
          <td style="width:17%; text-align:left">
            <span t-esc="amount_by_group[1]" t-options="{&quot;widget&quot;: &quot;monetary&quot;, &quot;display_currency&quot;: doc.pricelist_id.currency_id}"/>
          </td>
          <td style="width:14%; text-align:right">
            <Strong>Rechnungsbetrag</Strong>
          </td>
          <td style="width:18%; text-align:right">
            <span t-field="doc.amount_total"/>
          </td>
        </tr>
      </t>
    </table>
  </xpath>

</data>
```
Source: [snippets/sale.report_blanketorder_document.modify_main_table.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_blanketorder_document.modify_main_table.xml)

### Remove Informations  
ID: `mint_system.sale.report_blanketorder_document.remove_informations`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_blanketorder_document" priority="50">

<xpath expr="//div[@id='informations']" position="replace">
  </xpath>

</data>
```
Source: [snippets/sale.report_blanketorder_document.remove_informations.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_blanketorder_document.remove_informations.xml)

### Remove Summary Table  
ID: `mint_system.sale.report_blanketorder_document.remove_summary_table`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_blanketorder_document" priority="50">

<xpath expr="//div[@class='col-xs-4 pull-right']" position="replace">
</xpath>

</data>
```
Source: [snippets/sale.report_blanketorder_document.remove_summary_table.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_blanketorder_document.remove_summary_table.xml)

### Replace Addressblock  
ID: `mint_system.sale.report_blanketorder_document.replace_addressblock`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_blanketorder_document" priority="50">

  <xpath expr="//t/t/div/div[2]" position="replace">
    <t t-set="address">
            <div t-field="doc.partner_id" t-options="{&quot;widget&quot;: &quot;contact&quot;, &quot;fields&quot;: [&quot;address&quot;, &quot;name&quot;], &quot;no_marker&quot;: True}"/>
            <p t-if="doc.partner_id.vat"><t t-esc="doc.company_id.country_id.vat_label or 'Tax ID'"/>: <span t-field="doc.partner_id.vat"/></p>
    </t>
  </xpath>

</data>

```
Source: [snippets/sale.report_blanketorder_document.replace_addressblock.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_blanketorder_document.replace_addressblock.xml)

### Replace Infoblock  
ID: `mint_system.sale.report_blanketorder_document.replace_infoblock`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_blanketorder_document" priority="50">

    <xpath expr="//t/t/div/div[2]" position="replace">

        <div class="row" id="informations" style="font-size:16px; margin-bottom: 0rem">

            <div t-if="doc.client_order_ref" class="col-auto col-3 mw-100 mb-2">
                <strong>Your Reference</strong>
                <p t-field="doc.client_order_ref"/>
            </div>

            <div class="col-auto col-3 mw-100 mb-2">
                <strong>Order Date</strong>
                <p t-field="doc.create_date" t-options='{"widget": "date"}'/>
            </div>

            <div class="col-auto col-3 mw-100 mb-2">
                <strong>Validity Date</strong>
                <p t-field="doc.validity_date"/>
            </div>

            <div class="col-auto col-3 mw-100 mb-2">
                <strong>Incoterm</strong>
                <p t-field="doc.incoterm"/>
            </div>

            <div t-if="doc.user_id.name" class="col-auto col-3 mw-100 mb-2">
                <strong>Salesperson</strong>
                <p t-field="doc.user_id"/>
            </div>

        </div>
        
    </xpath>
    
</data>

```
Source: [snippets/sale.report_blanketorder_document.replace_infoblock.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_blanketorder_document.replace_infoblock.xml)

### Replace Table Attribute  
ID: `mint_system.sale.report_blanketorder_document.replace_table_attribute`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_blanketorder_document" priority="50">

  <xpath expr="//div[@class='col-xs-4 pull-right']" position="attributes">
    <attribute name="t-attf-class">#{'col-4' if report_type != 'html' else 'col-sm-7 col-md-5'} ml-auto</attribute>
  </xpath>

</data>

```
Source: [snippets/sale.report_blanketorder_document.replace_table_attribute.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_blanketorder_document.replace_table_attribute.xml)

### Replace Title  
ID: `mint_system.sale.report_blanketorder_document.replace_title`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_blanketorder_document" priority="50">

<xpath expr="//h2" position="replace">
    <h2>
      <span>Blanket Order # </span>
      <span t-field="doc.name"/>
    </h2>
</xpath>

</data>

```
Source: [snippets/sale.report_blanketorder_document.replace_title.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_blanketorder_document.replace_title.xml)

### Sequence In Table  
ID: `mint_system.sale.report_blanketorder_document.sequence_in_table`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_blanketorder_document" priority="50">

  <xpath expr="/t/t/div/table/thead/tr/th[1]" position="before">
    <th>
      <span>Pos</span>
    </th>

  <xpath expr="//table/tbody/t[2][@t-foreach='doc.order_line']" position="before">
    <t t-set="index" t-value="1"/>
  </xpath>

  </xpath>
  <xpath expr="/t/t/div/table/tbody/t[1]/tr[1]/td[1]" position="before">
    <td>
      <span t-esc="index"/><t t-set="index" t-value="index+1"/>
    </td>
  </xpath>

</data>

```
Source: [snippets/sale.report_blanketorder_document.sequence_in_table.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_blanketorder_document.sequence_in_table.xml)

### Set Ids  
ID: `mint_system.sale.report_blanketorder_document.set_ids`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_blanketorder_document" priority="50">
  
	<xpath expr="//div[1]/div[4]" position="attributes">
		<attribute name="id">table_total</attribute>
	</xpath>	

</data>
```
Source: [snippets/sale.report_blanketorder_document.set_ids.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_blanketorder_document.set_ids.xml)

## Report Purchaserequisitions  
### Add Adressblock  
ID: `mint_system.sale.report_purchaserequisitions.add_adressblock`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_purchaserequisitions" priority="50">

  <xpath expr="//div/div[1]" position="after">
    <div class="row address" style="font-size:16px; margin-bottom: 2rem">
      <div class="col-5"/>
      <div class="col-5 offset-2">
        <div t-field="o.vendor_id" t-options="{&quot;widget&quot;: &quot;contact&quot;, &quot;fields&quot;: [&quot;address&quot;, &quot;name&quot;], &quot;no_marker&quot;: True}"/>
      </div>
    </div>
  </xpath>

  <xpath expr="//div[1]/div[2]/div[2]/div[1]" position="attributes">
    <attribute name="t-options-fields">['name', 'address']</attribute>
  </xpath>

</data>

```
Source: [snippets/sale.report_purchaserequisitions.add_adressblock.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_purchaserequisitions.add_adressblock.xml)

### Add Description  
ID: `mint_system.sale.report_purchaserequisitions.add_description`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_purchaserequisitions" priority="49">

<xpath expr="//div/t[2]" position="after">
  <div style="font-size:16px; margin-top: 4rem">
    <p t-field="o.description"/>
  </div>
</xpath>

</data>

```
Source: [snippets/sale.report_purchaserequisitions.add_description.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_purchaserequisitions.add_description.xml)

### Remove Details  
ID: `mint_system.sale.report_purchaserequisitions.remove_details`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_purchaserequisitions" priority="55">

<xpath expr="//div/t[2]" position="replace">

</xpath>

</data>

```
Source: [snippets/sale.report_purchaserequisitions.remove_details.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_purchaserequisitions.remove_details.xml)

### Replace Infoblock  
ID: `mint_system.sale.report_purchaserequisitions.replace_infoblock`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_purchaserequisitions" priority="53">

  <xpath expr="//t/t/div/h2" position="after">

    <div class="row mt32 mb32" id="informations" style="font-size:16px; margin-bottom: 0rem">

                    <div t-if="o.origin" class="col-auto col-3 mw-100 mb-2">
                        <strong>Your Reference:</strong>
                        <p t-field="o.origin"/>
                    </div>

                    <div class="col-auto col-3 mw-100 mb-2">
                        <strong>Order Date:</strong>
                        <p t-field="o.create_date" t-options='{"widget": "date"}'/>
                    </div>

                    <div class="col-auto col-3 mw-100 mb-2">
                        <strong>Validity Date:</strong>
                        <p t-field="o.date_end" t-options='{"widget": "date"}'/>
                    </div>

                    <div class="col-auto col-3 mw-100 mb-2">
                        <strong>Salesperson:</strong>
                        <p t-field="o.create_uid"/>
                    </div>



                </div>
  </xpath>

  <xpath expr="//t/t/div/div[4]" position="replace">
  </xpath>

</data>

```
Source: [snippets/sale.report_purchaserequisitions.replace_infoblock.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_purchaserequisitions.replace_infoblock.xml)

### Replace Table  
ID: `mint_system.sale.report_purchaserequisitions.replace_table`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_purchaserequisitions" priority="49">

  <xpath expr="//div/t[1]" position="replace">
                        <t t-if="o.line_ids">

                        <table class="table table-sm">
                            <thead>
                                <tr>
                                    <th><strong>Description</strong></th>
                                    <th class="text-right"><strong>Qty</strong></th>

                                    <th class="text-right"><strong>Scheduled Date</strong></th>
                                    <th class="text-right"><strong>Unit Price</strong></th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr t-foreach="o.line_ids" t-as="line_ids">
                                    <td>
                                        [ <span t-field="line_ids.product_id.code"/> ]
                                        <span t-field="line_ids.product_id.name"/>
                                    </td>
                                    <td class="text-right">
                                        <span t-field="line_ids.product_qty"/> <span t-field="line_ids.product_uom_id.category_id.name"/>
                                    </td>
                                    <td class="text-right">
                                        <span t-field="line_ids.schedule_date"/>
                                    </td>

                                    <td class="text-right">
                                       <span t-field="line_ids.price_unit"/> <span t-field="o.currency_id"/>

                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </t>
   </xpath>
</data>

```
Source: [snippets/sale.report_purchaserequisitions.replace_table.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_purchaserequisitions.replace_table.xml)

### Sequence In Table  
ID: `mint_system.sale.report_purchaserequisitions.sequence_in_table`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_purchaserequisitions" priority="51">

  <xpath expr="//table/thead/tr[1]/th[1]" position="before">
    <th>
      <span>Pos</span>
    </th>

  <xpath expr="//table/tbody/tr[1]/td[1][@t-foreach='doc.order_line']" position="before">
    <t t-set="index" t-value="1"/>
  </xpath>

  </xpath>
  <xpath expr="//table/tbody/tr[1]/td[1]" position="before">
    <td>
      <span t-esc="index"/><t t-set="index" t-value="index+1"/>
    </td>
  </xpath>

</data>

```
Source: [snippets/sale.report_purchaserequisitions.sequence_in_table.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_purchaserequisitions.sequence_in_table.xml)

## Report Saleconfirmation  
### Base  
ID: `mint_system.sale.report_saleconfirmation.base`  
```xml
<?xml version="1.0"?>
<t t-name="sale.report_saleconfirmation.base">
    <t t-call="web.html_container">
        <t t-foreach="docs" t-as="doc">
            <t t-set="is_confirmation" t-value="True"/>
            <t t-call="sale.report_saleorder_document" t-lang="doc.partner_id.lang"/>
        </t>
    </t>
</t>
```
Source: [snippets/sale.report_saleconfirmation.base.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleconfirmation.base.xml)

## Report Saleorder Document  
### Add Delivery Date  
ID: `mint_system.sale.report_saleorder_document.add_delivery_date`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//div/table/thead/tr/th[4]" position="after">
    <th>
      <span>Del. Date</span>
    </th>
  </xpath>

  <xpath expr="//div/table/tbody/t[2]/tr/t[1]/td[4]" position="after">
    <td>
      <span t-field="line.commitment_date"/>
    </td>
  </xpath>

  <xpath expr="//div/table/tbody/t[2]/t[3]/tr/td" position="attributes">
    <attribute name="colspan">100</attribute>
  </xpath>

  <xpath expr="//div/table[1]/tbody[1]/t[2]/tr[1]/t[1]/td[5]/span[1]" position="attributes">
    <attribute name="t-options-widget">"date"</attribute>
  </xpath>

</data>

```
Source: [snippets/sale.report_saleorder_document.add_delivery_date.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.add_delivery_date.xml)

### Add Drawing  
ID: `mint_system.sale.report_saleorder_document.add_drawing`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="71">
  
  <xpath expr="//tbody//tr[1]" position="after">
    
    <tr style="padding:0">
            <t>
              <td style="padding:0; padding-left:3px; line-height: 1.2"></td>
              <td style="padding:0; padding-left:3px; line-height: 1.2"></td>
              <td style="padding:0; padding-left:3px; line-height: 1.2" colspan="4">
               <span t-field="line.name"/>
                <br/>
                Ursprungsland: <span t-field="line.product_id.country_of_origin_id.code"/> / Zollposition: <span t-field="line.product_id.hs_code"/>
              </td>
              <td></td>
            </t>
          </tr>
          <tr>
            <td></td>
          </tr>

   </xpath>
</data>
```
Source: [snippets/sale.report_saleorder_document.add_drawing.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.add_drawing.xml)

### Add Footer  
ID: `mint_system.sale.report_saleorder_document.add_footer`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

<xpath expr="//table[3]" position="after">
  <style>
      table#footer {
        width: 100%;
        font-size: 8pt;
      }
      table#footer tr, td {
        vertical-align: top;
      }
    </style>
    <table id='footer'>
      <tr>
        <td width="50%" t-if="doc.payment_term_id.note">Zahlungsbedingungen 
          <span t-field="doc.payment_term_id.note"/>
        </td>
         <td width="50%" t-if="not doc.payment_term_id.note">
        </td>
        
        <td width="50%">
          Lieferung gemäss unseren allgemeinen Lieferbedingungen
        </td>
      </tr>
      <tr>
        <td >MWST-Nr: 
           <span t-field="doc.company_id.vat"/>
        </td>
        <td>
          <table width="100%">
          <tr>
            <td width="35%">
               Bankverbindungen:
            </td>
              <td width="65%">
              UBS AG, 6301 Zug, BLZ 273, SWIFT UBSWCHZH80A
             </td>
          </tr> 
          <tr> 
             <td>
            </td>
            <td>
            (CHF) IBAN CH63 0027 3273 Q978 6962 0
            </td>
          </tr>
       
          <tr>
            <td>
            </td>
            <td>
            (EUR) IBAN CH59 0027 3273 HN10 3698 0
            </td>
          </tr>
          </table> 
        </td>
      </tr>
    </table>
  </xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.add_footer.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.add_footer.xml)

### Add Header And Footer Note  
ID: `mint_system.sale.report_saleorder_document.add_header_and_footer_note`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//table[@id='info']" position="after">
    <t t-if="doc.note_header != '&lt;p&gt;&lt;br&gt;&lt;/p&gt;'">
      <span class="note" t-field="doc.note_header"/>
    </t>
  </xpath>

  <xpath expr="//table[2]" position="after">
    <t t-if="doc.note_footer != '&lt;p&gt;&lt;br&gt;&lt;/p&gt;'">
      <span class="note" t-field="doc.note_footer"/>
    </t>
  </xpath>

</data>

```
Source: [snippets/sale.report_saleorder_document.add_header_and_footer_note.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.add_header_and_footer_note.xml)

### Add Header Space  
ID: `mint_system.sale.report_saleorder_document.add_header_space`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

	<xpath expr="//h2" position="attributes">
		 <attribute name="style">padding-top: 5rem</attribute>
	</xpath>

</data>

```
Source: [snippets/sale.report_saleorder_document.add_header_space.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.add_header_space.xml)

### Add Informations Space  
ID: `mint_system.sale.report_saleorder_document.add_informations_space`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

	<xpath expr="//div[@id='informations']" position="attributes">
		<attribute name="style">padding-top: 1rem</attribute>
		<attribute name="style">padding-bottom: 1rem</attribute>
	</xpath>

</data>

```
Source: [snippets/sale.report_saleorder_document.add_informations_space.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.add_informations_space.xml)

### Add Infotable  
ID: `mint_system.sale.report_saleorder_document.add_infotable`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//h2" position="after">
    <style>
      table#info {
        width: 100%;
        margin-bottom: 25px;
        font-size: 9pt;
        font-family: arial;
      }
        table#info tr {
        line-height: 1.2;
        text-align: left;
      }
        .note {
        font-size: 9pt;
      }
    </style>
    <table id='info'>
      <tr>
        <td width="17%">Date</td>
        <td width="40%">
          <span t-field='doc.date_order' t-options='{ "widget": "date" }'/>
        </td>
        <td width="18%">Our Reference</td>
        <td width="25%">
          <span t-field='doc.user_id'/>
        </td>
      </tr>
      <tr>
        <td>Customer No.</td>
        <td>
          <span t-field='doc.partner_id.ref'/>
        </td>
        <td>Delivery Method</td>
        <td>
          <span t-field='doc.carrier_id'/>
        </td>
      </tr>
      <tr>
        <td>Order</td>
        <td>
          <span t-field='doc.client_order_ref'/>
        </td>
        <td>Incoterm</td>
        <td>
          <span t-field='doc.incoterm'/>
        </td>
      </tr>
      <tr>
        <td>Reference</td>
        <td>
          <span t-field='doc.comment'/>
        </td>
        <t t-if="doc.blanket_order_id">
          <td>Blanket Order</td>
          <td>
            <span t-field='doc.blanket_order_id'/>
            <t t-if="doc.blanket_order_id.client_order_ref"> /              <span t-field='doc.blanket_order_id.client_order_ref'/>
            </t>
          </td>
        </t>
        <t t-else="">
          <td></td>
          <td></td>
        </t>
      </tr>
    </table>

  </xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.add_infotable.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.add_infotable.xml)

### Add Notes  
ID: `mint_system.sale.report_saleorder_document.add_notes`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="/t/t/div/div[2]" position="after">
    <t t-if="doc.note_header">
      <div class="row">
        <div class="col">
          <span t-field="doc.note_header"/>
          <br/>
        </div>
      </div>
    </t>
  </xpath>

  <xpath expr="/t/t/div/p[2]" position="before">
    <t t-if="doc.note_footer">
      <div class="row">
        <div class="col">
          <span t-field="doc.note_footer"/>
          <br/>
        </div>
      </div>
    </t>
  </xpath>

</data>

```
Source: [snippets/sale.report_saleorder_document.add_notes.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.add_notes.xml)

### Add Percentage Sign  
ID: `mint_system.sale.report_saleorder_document.add_percentage_sign`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

<xpath expr="//span[@t-field='line.discount']" position="replace">
    <span t-field="line.discount"/>%
  </xpath>

</data>

```
Source: [snippets/sale.report_saleorder_document.add_percentage_sign.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.add_percentage_sign.xml)

### Address Block  
ID: `mint_system.sale.report_saleorder_document.address_block`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <style>
      .address {
        font-size: 10pt;
        font-family: arial;
        line-height: 1.2;
        text-align: left;
      }
      .title {
        font-size: 8pt;
        font-weight: bold;
      }
      .margin {
        padding-bottom: 33mm;
      }
  </style>

  <xpath expr="//t[@t-set='address']/div" position="replace">
    <div class="address margin">
      <t t-if="doc.partner_contact_id">
        <div t-esc="doc.partner_contact_id.parent_id.name"/>
        <div t-esc="doc.partner_contact_id.parent_id.name2"/>
        <span t-esc="doc.partner_contact_id.title.name"/> <span t-esc="doc.partner_contact_id.name"/>
        <div t-esc="doc.partner_contact_id.street"/>
        <div t-esc="doc.partner_contact_id.street2"/>
        <span t-esc="doc.partner_contact_id.zip"/>
        <span t-esc="doc.partner_contact_id.city"/>
        <t t-if="doc.partner_contact_id.country_id.code != 'CH'">
          <div t-esc="doc.partner_contact_id.country_id.name"/>
        </t>
      </t>
      <t t-else="">
        <div t-field="doc.partner_id" t-options="{&quot;widget&quot;: &quot;contact&quot;, &quot;fields&quot;: [&quot;address&quot;, &quot;name&quot;], &quot;no_marker&quot;: True, &quot;phone_icons&quot;: False}" name="partner_contact_id"/>
      </t>
    </div>
  </xpath>

  <xpath expr="//t[@t-set='information_block']/../t" position="replace">
    <t class="address" t-set="information_block">
      <t t-if="doc.partner_shipping_id == doc.partner_invoice_id">
        <div class="title">Invoicing and Shipping Address:</div>
        <div t-field="doc.partner_shipping_id" t-options="{&quot;widget&quot;: &quot;contact&quot;, &quot;fields&quot;: [&quot;address&quot;, &quot;name&quot;], &quot;no_marker&quot;: True, &quot;phone_icons&quot;: False}"/>
      </t>
      <t t-if="doc.partner_shipping_id != doc.partner_invoice_id">
        <div class="title">Shipping Address:</div>
        <div t-field="doc.partner_shipping_id" t-options="{&quot;widget&quot;: &quot;contact&quot;, &quot;fields&quot;: [&quot;address&quot;, &quot;name&quot;], &quot;no_marker&quot;: True, &quot;phone_icons&quot;: False}"/>
      </t>
    </t>
  </xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.address_block.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.address_block.xml)

### Append Payment Terms  
ID: `mint_system.sale.report_saleorder_document.append_payment_terms`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="/t/t/div/div[6]" position="after">
    <div class="row">
      <div class="col">
        <strong>Zahlungsbedingungen: </strong>
        <span t-field="doc.payment_term_id.name"/>
      </div>
    </div>
  </xpath>

</data>

```
Source: [snippets/sale.report_saleorder_document.append_payment_terms.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.append_payment_terms.xml)

### Confirmation Filter Lines  
ID: `mint_system.sale.report_saleorder_document.confirmation_filter_lines`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//t[@t-foreach='doc.order_line']" position="attributes">
    <attribute name="t-foreach">doc.order_line.filtered(lambda l: not is_confirmation or (is_confirmation and l.qty_to_deliver > 0))</attribute>
  </xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.confirmation_filter_lines.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.confirmation_filter_lines.xml)

### Confirmation Header Quantity  
ID: `mint_system.sale.report_saleorder_document.confirmation_header_quantity`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//th[@name='th_quantity']" position="replace">
    <t t-if="is_confirmation">
      <th name="th_quantity" id="product_uom_qty" class="text-right">Backlog</th>
    </t>
    <t t-else="">
      <th name="th_quantity" id="product_uom_qty" class="text-right">Quantity</th>
    </t>
  </xpath>

</data> 
```
Source: [snippets/sale.report_saleorder_document.confirmation_header_quantity.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.confirmation_header_quantity.xml)

### Confirmation Qty To Deliver  
ID: `mint_system.sale.report_saleorder_document.confirmation_qty_to_deliver`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//td[@name='td_quantity']/span[1]" position="replace">
    <t t-if="is_confirmation">
      <span id="product_uom_qty_confirmed" t-esc="line.qty_to_deliver"/>
    </t>
    <t t-else="">
      <span id="product_uom_qty" t-esc="line.product_uom_qty"/>
    </t>
  </xpath>

  <xpath expr="//td[@name='td_subtotal']" position="replace">
    <t t-if="is_confirmation">
      <td name="td_subtotal" class="text-right o_price_total">
        <span t-esc="'%.2f' % (line.price_unit * line.qty_to_deliver * ((line.discount or 100.0) / 100.0))" groups="account.group_show_line_subtotals_tax_excluded"/>
        <span t-esc="'%.2f' % (line.price_unit * line.qty_to_deliver * ((line.discount or 100.0) / 100.0))" groups="account.group_show_line_subtotals_tax_included"/>
      </td>
    </t>
    <t t-else="">
      <td name="td_subtotal" class="text-right o_price_total">
        <span t-field="line.price_subtotal" groups="account.group_show_line_subtotals_tax_excluded"/>
        <span t-field="line.price_total" groups="account.group_show_line_subtotals_tax_included"/>
      </td>
    </t>
  </xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.confirmation_qty_to_deliver.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.confirmation_qty_to_deliver.xml)

### Confirmation Title  
ID: `mint_system.sale.report_saleorder_document.confirmation_title`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

    <xpath expr="//h2/t[1]" position="replace">
        <t t-if="not (env.context.get('proforma', False) or is_pro_forma)">
            <span t-if="is_confirmation">Confirmation # </span>
            <span t-if="doc.state not in ['draft','sent'] and not is_confirmation">Order # </span>
            <span t-if="doc.state in ['draft','sent'] and not is_confirmation">Quotation # </span>
        </t>
    </xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.confirmation_title.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.confirmation_title.xml)

### Expand Product Description  
ID: `mint_system.sale.report_saleorder_document.expand_product_description`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="56">

  <xpath expr="/t/t/div/table[2]/tbody/t[2]/tr/t[1]/td[3]/span" position="replace">
    <t>
      <span style="font-weight:bold;" t-field="line.product_id.type_description"/>
    </t>
     <t>
      <br/>
      <span t-field="line.product_id.name"/>
    </t><t>
      <br/>
      Ursprungsland: <span t-field="line.product_id.country_of_origin_id.code"/> / Zollposition: <span t-field="line.product_id.hs_code"/>
    </t>
   
  </xpath>
  
</data>
```
Source: [snippets/sale.report_saleorder_document.expand_product_description.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.expand_product_description.xml)

### Format Address Blocks  
ID: `mint_system.sale.report_saleorder_document.format_address_blocks`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//t[@t-set='address']/div" position="attributes">
    <attribute name="style">font-size:10pt; line-height: 1.2; padding-bottom:33mm</attribute>
  </xpath>

  <xpath expr="//t[@t-set='information_block']/strong[1]" position="attributes">
    <attribute name="style">font-size:10pt; line-height: 1.2;</attribute>
  </xpath>

  <xpath expr="//t[@t-set='information_block']/strong[2]" position="attributes">
    <attribute name="style">font-size:10pt; line-height: 1.2;</attribute>
  </xpath>

  <xpath expr="//t[@t-set='information_block']/div" position="attributes">
    <attribute name="style">font-size:10pt; line-height: 1.2;</attribute>
  </xpath>

  <xpath expr="//t[@t-set='information_block']/t/strong" position="attributes">
    <attribute name="style">font-size:10pt; line-height: 1.2;</attribute>
  </xpath>

  <xpath expr="//t[@t-set='information_block']/t/div" position="attributes">
    <attribute name="style">font-size:10pt; line-height: 1.2;</attribute>
  </xpath>

  <xpath expr="//t[@t-set='information_block']/div" position="attributes">
    <attribute name="t-options-fields">['address', 'name']</attribute>
  </xpath>

  <xpath expr="//t[@t-set='information_block']/t/div" position="attributes">
    <attribute name="t-options-fields">['address', 'name']</attribute>
  </xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.format_address_blocks.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.format_address_blocks.xml)

### Format As Date  
ID: `mint_system.sale.report_saleorder_document.format_as_date`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//div[1]/div[2]/div[2]/p[1]" position="attributes">
    <attribute name="t-options-widget">"date"</attribute>
  </xpath>

</data>

```
Source: [snippets/sale.report_saleorder_document.format_as_date.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.format_as_date.xml)

### Format Note  
ID: `mint_system.sale.report_saleorder_document.format_note`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//p[@t-field='doc.note']" position="attributes">
    <attribute name="style">font-size: 8pt</attribute>
  </xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.format_note.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.format_note.xml)

### Format Qty With Decimal  
ID: `mint_system.sale.report_saleorder_document.format_qty_with_decimal`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

	<xpath expr="//span[@id='product_uom_qty']" position="replace">
		<t t-if="line.product_uom.id == 1">
			<span id="product_uom_qty" t-field="line.product_uom_qty" t-options="{'widget': 'integer'}"/>
		</t>
		<t t-else="">
			<span id="product_uom_qty" t-field="line.product_uom_qty"/>
		</t>
	</xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.format_qty_with_decimal.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.format_qty_with_decimal.xml)

### Format Qty  
ID: `mint_system.sale.report_saleorder_document.format_qty`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

	<xpath expr="//span[@id='product_uom_qty']" position="attributes">
		<attribute name="t-options-widget">"integer"</attribute>
	</xpath>
	
	<xpath expr="//span[@id='product_uom_qty_confirmed']" position="attributes">
		<attribute name="t-options-widget">"integer"</attribute>
	</xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.format_qty.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.format_qty.xml)

### Format Title Trimada  
ID: `mint_system.sale.report_saleorder_document.format_title_trimada`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//h2" position="attributes">
    <attribute name="style">color: black; font-size:13pt; font-weight:bold; margin-top:10mm; margin-bottom:3mm</attribute>
  </xpath>
  
</data>
```
Source: [snippets/sale.report_saleorder_document.format_title_trimada.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.format_title_trimada.xml)

### Get Position  
ID: `mint_system.sale.report_saleorder_document.get_position`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//table/thead/tr/th[1]" position="before">
    <th id="position">
      <span>Pos</span>
    </th>
  </xpath>

  <!--
  <xpath expr="//table/tbody/t[2]/tr/t[1]/td[1]" position="before">
    <td id="position">
      <span t-field="line.position"/>
    </td>
  </xpath>
  -->

  <xpath expr="//span[@t-field='line.name']/.." position="before">
    <td id="position">
      <span t-field="line.position"/>
    </td>
  </xpath>

</data>

```
Source: [snippets/sale.report_saleorder_document.get_position.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.get_position.xml)

### Qty Remaining  
ID: `mint_system.sale.report_saleorder_document.qty_remaining`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//td[@name='td_quantity']" position="replace">
    <t t-set="blanket_line_ids" t-value="doc.blanket_order_id.line_ids.filtered(lambda r: r.product_id.id == line.product_id.id)" />
    <t t-set="remaining_qty" t-value="sum(blanket_line_ids.mapped('remaining_uom_qty'))" />

    <td name="td_quantity" class="text-right">
      <span t-field="line.product_uom_qty" />
      <span t-field="line.product_uom" />
      <t t-if="blanket_line_ids">
        /
        <t t-if="line.product_uom.id == 1">
         <span t-esc="'%.0f'%(remaining_qty)" />
        </t>
        <t t-else="">
          <span t-esc="'%.3f'%(remaining_qty)" />
        </t>
          <span t-field="line.product_uom" />        
      </t>
    </td>

  </xpath>

  <xpath expr="//th[@name='th_quantity']" position="replace">
    <th t-if="doc.blanket_order_id" name="th_quantity" class="text-right">Qty / Rem. Agreement Qty</th>
    <th t-if="not doc.blanket_order_id" name="th_quantity" class="text-right">Qty</th>
  </xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.qty_remaining.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.qty_remaining.xml)

### Remove Informations  
ID: `mint_system.sale.report_saleorder_document.remove_informations`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

<xpath expr="//div[@id='informations']" position="replace">
  </xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.remove_informations.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.remove_informations.xml)

### Remove Payment Terms  
ID: `mint_system.sale.report_saleorder_document.remove_payment_terms`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

<xpath expr="//p[@t-if='doc.payment_term_id.note']" position="replace">
</xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.remove_payment_terms.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.remove_payment_terms.xml)

### Remove Summary Table  
ID: `mint_system.sale.report_saleorder_document.remove_summary_table`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

<xpath expr="//div[2]" position="replace">
</xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.remove_summary_table.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.remove_summary_table.xml)

### Remove Taxes  
ID: `mint_system.sale.report_saleorder_document.remove_taxes`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//th[@name='th_taxes']" position="replace"/>
  <xpath expr="//td[@name='td_taxes']" position="replace"/>

</data>
```
Source: [snippets/sale.report_saleorder_document.remove_taxes.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.remove_taxes.xml)

### Remove Vat  
ID: `mint_system.sale.report_saleorder_document.remove_vat`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

<xpath expr="//p[@t-if='doc.partner_id.vat']" position="replace"/>

</data>
```
Source: [snippets/sale.report_saleorder_document.remove_vat.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.remove_vat.xml)

### Rename Order  
ID: `mint_system.sale.report_saleorder_document.rename_order`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//table[1]/thead[1]/tr[1]/th[5]" position="replace"/>
  <xpath expr="//table[1]/tbody[1]/t[2]/tr[1]/t[1]/td[5]" position="replace"/>

</data>

```
Source: [snippets/sale.report_saleorder_document.rename_order.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.rename_order.xml)

### Rename Proforma Title  
ID: `mint_system.sale.report_saleorder_document.rename_proforma_title`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//h2/t[2]/span" position="replace">
    <!-- <span>Auftragsbestätigung # </span> -->
    <span>Order Confirmation # </span>
  </xpath>
  
</data>
```
Source: [snippets/sale.report_saleorder_document.rename_proforma_title.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.rename_proforma_title.xml)

### Rename Table Header  
ID: `mint_system.sale.report_saleorder_document.rename_table_header`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//div/table/thead/tr/th[2]" position="replace">
    <th class="text-left">Comm. Date</th>
  </xpath>

  <xpath expr="//div/table/thead/tr/th[6]" position="replace">
    <th name="th_priceunit" class="text-right">U. Price</th>
  </xpath>

</data>

```
Source: [snippets/sale.report_saleorder_document.rename_table_header.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.rename_table_header.xml)

### Replace Partner Id  
ID: `mint_system.sale.report_saleorder_document.replace_partner_id`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

 <xpath expr="//t[@t-set='address']/div" position="replace">
    <div style="font-size:10pt; line-height: 1.2; padding-bottom:33mm">
      <t t-if="doc.partner_contact_id.parent_name">
        <div t-field="doc.partner_contact_id" t-options="{&quot;widget&quot;: &quot;contact&quot;, &quot;fields&quot;: [&quot;address&quot;, &quot;name&quot;], &quot;no_marker&quot;: True, &quot;phone_icons&quot;: False}" name="partner_contact_id"/>
      </t>
      <t t-if="not doc.partner_contact_id.parent_name">
        <div t-field="doc.partner_contact_id" t-options="{&quot;widget&quot;: &quot;contact&quot;, &quot;fields&quot;: [&quot;address&quot;, &quot;name&quot;], &quot;no_marker&quot;: True, &quot;phone_icons&quot;: False}" name="partner_contact_id"/>
      </t>
    </div>
  </xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.replace_partner_id.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.replace_partner_id.xml)

### Replace Product Description  
ID: `mint_system.sale.report_saleorder_document.replace_product_description`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//td[@name='td_name']" position="replace">
    <t t-if="line.product_id.type_description">
      <td>
        <span class="o_bold" t-field="line.product_id.type_description" />
      </td>
    </t>
    <t t-if="not line.product_id.type_description">
      <td>
        <span t-field="line.name" />
      </td>
    </t>

  </xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.replace_product_description.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.replace_product_description.xml)

### Replace Summary  
ID: `mint_system.sale.report_saleorder_document.replace_summary`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//div[@name='so_total_summary']" position="replace">

    <style>
			table.trimada_summary tr {
				border-top: solid 1px !important;
				border-bottom: solid 1px;
			}
			table.trimada_details tr {
			  border-top: 0px !important;
			  border-bottom: 0px;
			  line-height: 0.7;
			}
			table.trimada_summary #amount_untaxed_label {
				width: 15.5%;
				text-align: left;
			}
			table.trimada_summary #amount_untaxed {
				width: 23%;
				text-align: left;
			}
			table.trimada_summary #amount_by_group_label {
				width: 12%;
				text-align: left;
			}
			table.trimada_summary #amount_by_group {
				width: 17%;
				text-align: left;
			}
			table.trimada_summary #current_subtotal_label {
				width: 14%;
				text-align: right;
			}
			table.trimada_summary #current_subtotal {
				width: 18%;
				text-align: right;
			}
    </style>

    <table class="table table-borderless table-sm trimada trimada_summary o_main_table">
      <tr>
        <td id="amount_untaxed_label">
          <strong>Warenwert</strong>
        </td>
        <td id="amount_untaxed">
          <span t-field="doc.amount_untaxed"/>
        </td>

        <td>
          <table class="trimada_details">
            <t t-foreach="doc.amount_by_group" t-as="amount_by_group">
                <tr style="">
                  <t t-if="amount_by_group[5] == 1 and doc.amount_untaxed == amount_by_group[2]">
                    <td name="td_amount_by_group_label_3">
                      <span t-esc="amount_by_group[0]"/>
                      </td>
                    <td name="td_amount_by_group_3" class="text-right o_price_total">
                      <span t-esc="amount_by_group[1]" t-options="{&quot;widget&quot;: &quot;monetary&quot;, &quot;display_currency&quot;: doc.pricelist_id.currency_id}"/>
                    </td>
                  </t>
                  <t t-else="">
                    <td name="td_amount_by_group_label">
                      <span t-esc="amount_by_group[0]"/>
                    </td>
                    <td name="td_amount_by_group" class="text-right o_price_total">
                      <span t-esc="amount_by_group[1]" t-options="{&quot;widget&quot;: &quot;monetary&quot;, &quot;display_currency&quot;: doc.pricelist_id.currency_id}"/>
                    </td>
                  </t>
                </tr>
            </t>
          </table>
        </td>

        <td id="current_subtotal_label">
          <strong>Rechnungsbetrag</strong>
        </td>
        <td id="current_subtotal">
          <span t-field="doc.amount_total"/>
        </td>
      </tr>
    </table>

  </xpath>
</data>
```
Source: [snippets/sale.report_saleorder_document.replace_summary.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.replace_summary.xml)

### Round Price2  
ID: `mint_system.sale.report_saleorder_document.round_price2`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//span[@t-field='line.price_unit']" position="replace">
    <!-- 34.00 -> 34 -->
    <!-- 34.50 -> 34.50 -->
    <!-- 34.75 -> 34.75 -->
    <span t-esc="'%g' % line.price_unit if int(line.price_unit) == line.price_unit else '%.2f' % line.price_unit" />
  </xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.round_price2.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.round_price2.xml)

### Round Price  
ID: `mint_system.sale.report_saleorder_document.round_price`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//span[@t-field='line.price_unit']" position="replace">
     <span t-esc="'%g' % line.price_unit if str(line.price_unit)[::-1].find('.') >= 3 else '%.2f' % line.price_unit" /> 
  </xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.round_price.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.round_price.xml)

### Round Total Price  
ID: `mint_system.sale.report_saleorder_document.round_total_price`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="60">

  <xpath expr="//span[@t-field='line.price_subtotal']" position="replace">
    <span t-esc="'{0:,.2f}'.format(float(line.price_subtotal)).replace(',','\'')"/>
  </xpath>

</data>

```
Source: [snippets/sale.report_saleorder_document.round_total_price.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.round_total_price.xml)

### Second Row  
ID: `mint_system.sale.report_saleorder_document.second_row`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">
  
  <xpath expr="//tbody[hasclass('sale_tbody')]/t/tr[1]" position="attributes">
    <attribute name="t-att-class">"first"</attribute>
  </xpath>

  <xpath expr="//tbody[hasclass('sale_tbody')]/t/tr[1]" position="after">
    <t t-if="line.product_id.type_description">
    <tr class="second">
      <td></td>
      <td></td>
      <td colspan="6">
        <span t-field="line.name"/><br/>
        <t t-if="line.product_id.country_of_origin_id.code">
          Ursprungsland:
          <span t-field="line.product_id.country_of_origin_id.code" />
        </t>
        <t t-if="line.product_id.hs_code">
          / Zollposition:
          <span t-field="line.product_id.hs_code" />
        </t>
      </td>
    </tr>
    </t>
    <t t-if="not line.product_id.type_description">
    <tr class="second">
      <td></td>
      <td></td>
      <td colspan="6">
        <t t-if="line.product_id.country_of_origin_id.code">
          Ursprungsland:
          <span t-field="line.product_id.country_of_origin_id.code" />
        </t>
        <t t-if="line.product_id.hs_code">
          / Zollposition:
          <span t-field="line.product_id.hs_code" />
        </t>
      </td>
    </tr>
    </t>
  </xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.second_row.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.second_row.xml)

### Sequence In Table  
ID: `mint_system.sale.report_saleorder_document.sequence_in_table`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="/t/t/div/table/thead/tr/th[1]" position="before">
    <th>
      <span>Pos</span>
    </th>

  <xpath expr="//table/tbody/t[2][@t-foreach='doc.order_line']" position="before">
    <t t-set="index" t-value="1"/>
  </xpath>

  </xpath>
  <xpath expr="/t/t/div/table/tbody/t[2]/tr/t[1]/td[1]" position="before">
    <td>
      <span t-esc="index"/><t t-set="index" t-value="index+1"/>
    </td>
  </xpath>

</data>

```
Source: [snippets/sale.report_saleorder_document.sequence_in_table.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.sequence_in_table.xml)

### Set Ids  
ID: `mint_system.sale.report_saleorder_document.set_ids`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

	<xpath expr="//th[@name='th_description']" position="attributes">
		<attribute name="id">description</attribute>
	</xpath>

	<xpath expr="//th[@name='th_quantity']" position="attributes">
		<attribute name="id">product_uom_qty</attribute>
	</xpath>

	<xpath expr="//td[@name='td_quantity']/span[1]" position="attributes">
		<attribute name="id">product_uom_qty</attribute>
	</xpath>
	
	<xpath expr="//td[@name='td_quantity']/span[2]" position="attributes">
		<attribute name="id">product_uom</attribute>
	</xpath>

	<xpath expr="//td[@name='td_quantity']" position="attributes">
		<attribute name="id">product_uom_qty</attribute>
	</xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.set_ids.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.set_ids.xml)

### Show Default Code  
ID: `mint_system.sale.report_saleorder_document.show_default_code`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">
 
  <xpath expr="//table[2]/thead/tr/th[1]" position="after">
    <th id="default_code">
      <strong >Part No.</strong>
    </th>
  </xpath>

  <xpath expr="//table[2]/tbody/t/tr/t[1]/td[1]" position="after">
    <td id="default_code">
      <span t-field="line.product_id.default_code"/>
    </td>
  </xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.show_default_code.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.show_default_code.xml)

### Show Partner Contact Id  
ID: `mint_system.sale.report_saleorder_document.show_partner_contact_id`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//div[@t-field='doc.partner_id']" position="replace">
    <t t-if="doc.partner_contact_id">
      <div t-field="doc.partner_contact_id" t-options="{&quot;widget&quot;: &quot;contact&quot;, &quot;fields&quot;: [&quot;address&quot;, &quot;name&quot;], &quot;no_marker&quot;: True, &quot;phone_icons&quot;: False}" />
    </t>
    <t t-if="not doc.partner_contact_id">
      <div t-field="doc.partner_id" t-options="{&quot;widget&quot;: &quot;contact&quot;, &quot;fields&quot;: [&quot;address&quot;, &quot;name&quot;], &quot;no_marker&quot;: True, &quot;phone_icons&quot;: False}" />
    </t>
  </xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.show_partner_contact_id.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.show_partner_contact_id.xml)

### Style Trimada  
ID: `mint_system.sale.report_saleorder_document.style_trimada`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="60">

	<xpath expr="//div[hasclass('page')]" position="before">
		<style>
			.o_company_1_layout {
				font-family: arial;
			}
			table.trimada {
				font-size: 9pt;
				font-family: arial;
				color: black;
			}
			table.trimada tr.first td {
				padding-bottom: 0;
			}
			table.trimada tr.second td {
				padding-top: 0;
			}
			table.trimada tr.second {
				border-bottom: 1px solid rgb(220,220,220);
			}
			table.trimada thead tr {
				border-top:solid 1px;
				border-bottom: solid 1px;
			}
			table.trimada thead th#position {
				width: 5mm;
			}
			table.trimada thead th#default_code {
			  width: 27mm;
			  text-align: right;
			}
			table.trimada thead th#quantity {
			  width: 25mm;
			  text-align: right !important;
			}
			table.trimada tbody td#position {
			  text-align: right;
			}
			table.trimada tbody td#default_code {
			  text-align: right;
			}
			table.trimada tbody #commitment_date {
			  text-align: right;
			}
			table.trimada tbody td span#product_uom_qty {
			  font-weight: bold;
			}
			table.trimada tbody td span#product_uom_qty_confirmed {
			  font-weight: bold;
			}
			.subtitel {
				font-size: 11pt;
				font-family: arial;
				margin-top: 10mm;
			}
			.note {
				font-size: 9pt;
				font-family: arial;
			}
		</style>
	</xpath>

	<xpath expr="//table[2]" position="attributes">
		<attribute name="class" separator=" " add="trimada table-borderless"/>
	</xpath>
	
	<xpath expr="//th[@id='commitment_date']" position="attributes">
		<attribute name="class">text-right</attribute>
	</xpath>

</data>


```
Source: [snippets/sale.report_saleorder_document.style_trimada.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.style_trimada.xml)

### X Hide On Sale Order  
ID: `mint_system.sale.report_saleorder_document.x_hide_on_sale_order`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

	  <xpath expr="//t[@t-foreach='doc.order_line']" position="attributes">
		<attribute name="t-foreach">doc.order_line.filtered(lambda l: not l.product_id.x_hide_on_sale_order)</attribute>
	  </xpath>

</data>
```
Source: [snippets/sale.report_saleorder_document.x_hide_on_sale_order.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.x_hide_on_sale_order.xml)

### X Sudio Description  
ID: `mint_system.sale.report_saleorder_document.x_sudio_description`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_document" priority="50">

  <xpath expr="//tbody[hasclass('sale_tbody')]/t[2]/tr/t[1]/td[1]/span" position="before">
    <span t-field="line.product_id.name"/>
  </xpath>

  <xpath expr="//tbody[hasclass('sale_tbody')]/t[2]/tr/t[1]/td[1]/span[1]" position="after">
    <span>
      <br/>
    </span>
  </xpath>

  <xpath expr="//tbody[hasclass('sale_tbody')]/t[2]/tr/t[1]/td[1]/span[3]" position="attributes">
    <attribute name="class" separator=" " add="o_italic"/>
  </xpath>

  <xpath expr="/t/t/div/div[2]" position="after">
    <t t-if="doc.x_studio_description">
      <div class="row">
        <div class="col">
          <span t-field="doc.x_studio_description"/>
          <br/>
          <br/>
        </div>
      </div>
    </t>
  </xpath>

  <xpath expr="//tbody[hasclass('sale_tbody')]/tr/td[1]/span" position="attributes">
    <attribute name="class" separator=" " add="o_italic"/>
  </xpath>

  <xpath expr="//tbody[hasclass('sale_tbody')]/tr/td[1]/span" position="before">
    <span t-field="option.product_id.name"/>
  </xpath>

  <xpath expr="//tbody[hasclass('sale_tbody')]/tr/td[1]/span" position="after">
    <span>
      <br/>
    </span>
  </xpath>

  <xpath expr="/t/t/div/div[6]" position="after">
    <div class="row">
      <div class="col h2">
        <span>New Title</span>
      </div>
    </div>
  </xpath>

  <xpath expr="/t[1]/t[1]/div[1]/div[7]/div[1]" position="attributes">
    <attribute name="class">col h4</attribute>
  </xpath>

  <xpath expr="/t/t/div/div[7]/div/span" position="replace">
    <p style="page-break-before:always;"/>
    <span>Geschäftsbedingungen</span>
  </xpath>

  <xpath expr="/t/t/div/div[2]/div[5]/p" position="attributes">
    <attribute name="style" separator=";" add="width:150px"/>
  </xpath>
</data>

```
Source: [snippets/sale.report_saleorder_document.x_sudio_description.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_document.x_sudio_description.xml)

## Report Saleorder Pro Forma  
### Append Signature  
ID: `mint_system.sale.report_saleorder_pro_forma.append_signature`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.report_saleorder_pro_forma" priority="50">

  <xpath expr="/t/t/div/table/tbody/t[2]/tr/t[1]/td[1]/span" position="after">
    <t t-if="is_pro_forma">
      <t t-if="line.product_id.hs_code">
        <br/>
        <span>Zolltarifnummer: </span>
        <span t-field="line.product_id.hs_code"/>
      </t>
    </t>
  </xpath>
  <xpath expr="/t/t/div/p[2]" position="after">
    <t t-if="is_pro_forma">
        <span>
          <p>Der Unterzeichner erklärt, dass die in diesem Dokument aufgeführten Waren und Ursprungserzeugnisse der Schweiz sind und den Ursprungsregeln im Präferenzverkehr mit der EU entsprechen.<br/><br/></p>
          <p>Unterschrift: _______________________    Datum: _______________________<br/>                        Velo Manufaktur AG<br/></p>
        </span>
    </t>
  </xpath>
</data>

```
Source: [snippets/sale.report_saleorder_pro_forma.append_signature.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.report_saleorder_pro_forma.append_signature.xml)

## Sale Order Portal Content  
### Description  
ID: `mint_system.sale.sale_order_portal_content.description`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.sale_order_portal_content" priority="50">

  <xpath expr="//div[@id='informations']" position="after">
    <p t-field="sale_order.x_studio_description" />
  </xpath>

</data>

```
Source: [snippets/sale.sale_order_portal_content.description.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.sale_order_portal_content.description.xml)

### Product Name  
ID: `mint_system.sale.sale_order_portal_content.product_name`  
```xml
<?xml version="1.0"?>
<!-- Add product name to quote -->
<data inherit_id="sale.sale_order_portal_content" priority="50">

  <xpath expr="//td[@id='product_name']" position="replace">
  	<td id="product_name"><span t-field="line.product_id.name"/><br/><span class="font-italic" t-field="line.name"/></td>
  </xpath>

</data>

```
Source: [snippets/sale.sale_order_portal_content.product_name.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.sale_order_portal_content.product_name.xml)

### Remove Calculation  
ID: `mint_system.sale.sale_order_portal_content.remove_calculation`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.sale_order_portal_content" priority="50">

  <xpath expr="//table/thead/tr/th[6]" position="replace">
  </xpath>
  <xpath expr="//table/thead/tr/th[5]" position="replace">
  </xpath>
  <xpath expr="//table/thead/tr/th[4]" position="replace">
  </xpath>
  <xpath expr="//table/thead/tr/th[3]" position="replace">
  </xpath>

  <xpath expr="//table/tbody/t[2]/tr/t[1]/td[6]" position="replace">
  </xpath>
  <xpath expr="//table/tbody/t[2]/tr/t[1]/td[5]" position="replace">
  </xpath>
  <xpath expr="//table/tbody/t[2]/tr/t[1]/td[4]" position="replace">
  </xpath>
  <xpath expr="//table/tbody/t[2]/tr/t[1]/td[3]" position="replace">
  </xpath>

</data>

```
Source: [snippets/sale.sale_order_portal_content.remove_calculation.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.sale_order_portal_content.remove_calculation.xml)

## Sale Order View Search Inherit Quotation  
### Add Filter Cancel  
ID: `mint_system.sale.sale_order_view_search_inherit_quotation.add_filter_cancel`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.sale_order_view_search_inherit_quotation" priority="50">

  <xpath expr="//filter[@name='sales']" position="after">
     <filter string="Abgebrochen" name="cancel" domain="[('state','=','cancel')]"/>
  </xpath>

</data>
```
Source: [snippets/sale.sale_order_view_search_inherit_quotation.add_filter_cancel.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.sale_order_view_search_inherit_quotation.add_filter_cancel.xml)

### Add Filter Sent  
ID: `mint_system.sale.sale_order_view_search_inherit_quotation.add_filter_sent`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.sale_order_view_search_inherit_quotation" priority="50">

  <xpath expr="//filter[@name='sales']" position="after">
     <filter string="Gesendet" name="sent" domain="[('state','=','sent')]"/>
  </xpath>

</data>
```
Source: [snippets/sale.sale_order_view_search_inherit_quotation.add_filter_sent.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.sale_order_view_search_inherit_quotation.add_filter_sent.xml)

### Add Filter State Draft Or Sent  
ID: `mint_system.sale.sale_order_view_search_inherit_quotation.add_filter_state_draft_or_sent`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.sale_order_view_search_inherit_quotation" priority="50">

  <xpath expr="//filter[@name='my_quotation']" position="after">
    <filter string="Meine Angebote im Status Angebot oder Gesendet" name="state_draft_or_sent" domain="['&amp;',('user_id', '=', uid),('state','in',('draft', 'sent'))]"/>
  </xpath>

</data>
```
Source: [snippets/sale.sale_order_view_search_inherit_quotation.add_filter_state_draft_or_sent.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.sale_order_view_search_inherit_quotation.add_filter_state_draft_or_sent.xml)

## Sale Order View Search Inherit Sale  
### Add Invoice Status Invoiced  
ID: `mint_system.sale.sale_order_view_search_inherit_sale.add_invoice_status_invoiced`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.sale_order_view_search_inherit_sale" priority="50">

  <xpath expr="//filter[@name='to_invoice']" position="after">
     <filter string="Komplett abgerechnet" name="invoice_status_no" domain="[('invoice_status','=','invoiced')]"/>
  </xpath>

</data>
```
Source: [snippets/sale.sale_order_view_search_inherit_sale.add_invoice_status_invoiced.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.sale_order_view_search_inherit_sale.add_invoice_status_invoiced.xml)

### Add Invoice Status No  
ID: `mint_system.sale.sale_order_view_search_inherit_sale.add_invoice_status_no`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.sale_order_view_search_inherit_sale" priority="50">

  <xpath expr="//filter[@name='to_invoice']" position="after">
     <filter string="Nichts abzurechnen" name="invoice_status_no" domain="[('invoice_status','=','no')]"/>
  </xpath>

</data>
```
Source: [snippets/sale.sale_order_view_search_inherit_sale.add_invoice_status_no.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.sale_order_view_search_inherit_sale.add_invoice_status_no.xml)

### Add Invoice Status To Invoice Or No  
ID: `mint_system.sale.sale_order_view_search_inherit_sale.add_invoice_status_to_invoice_or_no`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.sale_order_view_search_inherit_sale" priority="50">

  <xpath expr="//filter[@name='my_sale_orders_filter']" position="after">
     <filter string="Abzurechnen oder Nichts abzurechnen" name="invoice_status_to_invoice_or_no" domain="[('invoice_status','in',('to invoice', 'no'))]"/>
  </xpath>

</data>
```
Source: [snippets/sale.sale_order_view_search_inherit_sale.add_invoice_status_to_invoice_or_no.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.sale_order_view_search_inherit_sale.add_invoice_status_to_invoice_or_no.xml)

### Filter Commitment Date  
ID: `mint_system.sale.sale_order_view_search_inherit_sale.filter_commitment_date`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.sale_order_view_search_inherit_sale" priority="50">

  <filter name="order_date" position="after">
    <filter string="Liefertermin" name="date_commitment" date="commitment_date" />
  </filter>
  
</data>
```
Source: [snippets/sale.sale_order_view_search_inherit_sale.filter_commitment_date.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.sale_order_view_search_inherit_sale.filter_commitment_date.xml)

## Variants  
### Remove Variant Extra Price  
ID: `mint_system.sale.variants.remove_variant_extra_price`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.variants" priority="50">

    <xpath expr="//span[hasclass('variant_price_extra')]" position="before">
        <style>
            li.variant_attribute .badge {
                display: none;
            }
        </style>
    </xpath>

</data>
```
Source: [snippets/sale.variants.remove_variant_extra_price.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.variants.remove_variant_extra_price.xml)

## View Order Form  
### Add Blanket Order Id  
ID: `mint_system.sale.view_order_form.add_blanket_order_id`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_form" priority="50">

  <xpath expr="//field[@name='tag_ids']" position="after">
    <field name="blanket_order_id"/>
  </xpath>

</data>
```
Source: [snippets/sale.view_order_form.add_blanket_order_id.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_form.add_blanket_order_id.xml)

### Button Recompute Add Shipping  
ID: `mint_system.sale.view_order_form.button_recompute_add_shipping`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_form" priority="50">

  <button name="action_open_delivery_wizard" position="attributes">
    <attribute name="context">{'carrier_recompute':True}</attribute>
  </button>

</data>

```
Source: [snippets/sale.view_order_form.button_recompute_add_shipping.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_form.button_recompute_add_shipping.xml)

### Domain Partner Type  
ID: `mint_system.sale.view_order_form.domain_partner_type`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_form" priority="50">

  <xpath expr="//group[@name='sale_header']/group/field[@name='partner_id']" position="attributes">
    <attribute name="domain">[('type', 'not in', ['invoice', 'delivery'])]</attribute>
  </xpath>

</data>

```
Source: [snippets/sale.view_order_form.domain_partner_type.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_form.domain_partner_type.xml)

### Edit Name  
ID: `mint_system.sale.view_order_form.edit_name`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_form" priority="50">

  <xpath expr="//field[@name='name']" position="attributes">
    <attribute name="readonly">0</attribute>
    <attribute name="attrs">{'readonly': [('project_id', '=', False)]}</attribute>
  </xpath>

</data>

```
Source: [snippets/sale.view_order_form.edit_name.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_form.edit_name.xml)

### Filter Customer Is Company  
ID: `mint_system.sale.view_order_form.filter_customer_is_company`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_form" priority="50">

  <xpath expr="//group[1]/group[1]/field[1]" position="replace">
    <field name="partner_id" widget="res_partner_many2one" domain="[('is_company', '=', True)]" context="{'res_partner_search_mode': 'customer', 'show_address': 1, 'show_vat': True, 'default_is_company': 'True'}" options="{&quot;always_reload&quot;: True}"/>
  </xpath>

</data>

```
Source: [snippets/sale.view_order_form.filter_customer_is_company.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_form.filter_customer_is_company.xml)

### Format Dates  
ID: `mint_system.sale.view_order_form.format_dates`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_form" priority="50">

  <xpath expr="//field[3][@name='date_order']" position="attributes">
    <attribute name="widget">date</attribute>
  </xpath>
  <xpath expr="//div/field[@name='commitment_date']" position="attributes">
    <attribute name="widget">date</attribute>
  </xpath>
  <xpath expr="//field[@name='order_line']/tree/field[@name='commitment_date']" position="attributes">
      <attribute name="widget">date</attribute>
  </xpath>

</data>

```
Source: [snippets/sale.view_order_form.format_dates.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_form.format_dates.xml)

### Header Delivery Date  
ID: `mint_system.sale.view_order_form.header_delivery_date`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_form" priority="50">

  <field name="date_order" position="after">
    <field name="commitment_date"/>
  </field>

</data>

```
Source: [snippets/sale.view_order_form.header_delivery_date.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_form.header_delivery_date.xml)

### Hide Validity Date  
ID: `mint_system.sale.view_order_form.hide_validity_date`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_form" priority="50">

  <field name="validity_date" position="replace">
  </field>

</data>

```
Source: [snippets/sale.view_order_form.hide_validity_date.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_form.hide_validity_date.xml)

### Modify Readonly Date Order  
ID: `mint_system.sale.view_order_form.modify_readonly_date_order`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_form" priority="50">

  <xpath expr="//field[@name='date_order'][2]" position="attributes">
      <attribute name="attrs">{"invisible": [["state","in",["draft","sent"]]], "readonly": [["state","not in",["draft","sent","sale"]]], "required": [["state","in",["sale","done"]]]}</attribute>
  </xpath>

</data>
```
Source: [snippets/sale.view_order_form.modify_readonly_date_order.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_form.modify_readonly_date_order.xml)

### No Create Edit  
ID: `mint_system.sale.view_order_form.no_create_edit`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_form" priority="50">

  <xpath expr="//field[@name='partner_id']" position="attributes">
    <attribute name="options">{'always_reload': True, 'no_quick_create': True, 'no_create_edit': True}</attribute>
  </xpath>

  <xpath expr="//field[@name='product_id']" position="attributes">
    <attribute name="widget">selection</attribute>
  </xpath>

</data>

```
Source: [snippets/sale.view_order_form.no_create_edit.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_form.no_create_edit.xml)

### Remove Margin Percent  
ID: `mint_system.sale.view_order_form.remove_margin_percent`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_form" priority="50">

    <xpath expr="//field[@name='margin_percent']" position="replace" />

</data>

```
Source: [snippets/sale.view_order_form.remove_margin_percent.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_form.remove_margin_percent.xml)

### Show Carrier Method  
ID: `mint_system.sale.view_order_form.show_carrier_method`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_form" priority="50">

  <field name="payment_term_id" position="after">
    <field name="carrier_id"/>
  </field>

</data>

```
Source: [snippets/sale.view_order_form.show_carrier_method.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_form.show_carrier_method.xml)

### Show Order Line Project Id  
ID: `mint_system.sale.view_order_form.show_order_line_project_id`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_form" priority="50">

  <xpath expr="//field[@name='order_line']/tree/field[@name='product_id']" position="after">
    <field name="project_id" optional="hide" />
  </xpath>

</data>
```
Source: [snippets/sale.view_order_form.show_order_line_project_id.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_form.show_order_line_project_id.xml)

### Show Project  
ID: `mint_system.sale.view_order_form.show_project`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_form" priority="50">

  <field name="partner_id" position="after">
    <field name="project_id"/>
  </field>

</data>

```
Source: [snippets/sale.view_order_form.show_project.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_form.show_project.xml)

### Show Purchase Line Count  
ID: `mint_system.sale.view_order_form.show_purchase_line_count`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_form" priority="50">

  <xpath expr="//field[@name='order_line']/tree//field[@name='price_unit']" position="after">
    <field name="purchase_line_count" optional="hide"/>
  </xpath>

</data>

```
Source: [snippets/sale.view_order_form.show_purchase_line_count.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_form.show_purchase_line_count.xml)

### Show Purchase Line Ids  
ID: `mint_system.sale.view_order_form.show_purchase_line_ids`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_form" priority="50">

  <xpath expr="//field[@name='order_line']/tree//field[@name='price_unit']" position="after">
    <field name="purchase_line_ids" optional="hide" widget="many2many_tags"/>
  </xpath>

</data>

```
Source: [snippets/sale.view_order_form.show_purchase_line_ids.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_form.show_purchase_line_ids.xml)

### Show Stock Purchase Line Ids  
ID: `mint_system.sale.view_order_form.show_stock_purchase_line_ids`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_form" priority="50">

  <xpath expr="//field[@name='order_line']/tree/field[@name='price_unit']" position="after">
    <field name="stock_purchase_line_ids" widget="many2many_tags" optional="hide" />
  </xpath>

</data>
```
Source: [snippets/sale.view_order_form.show_stock_purchase_line_ids.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_form.show_stock_purchase_line_ids.xml)

### X Drawing File  
ID: `mint_system.sale.view_order_form.x_drawing_file`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_form" priority="50">

  <xpath expr="//field[@name='order_line']/tree[1]/field[@name='name']" position="after">
    <field name="x_drawing_file"/>
  </xpath>

  <xpath expr="//field[@name='order_line']/form[1]//field[@name='name']" position="after">
    <label for="x_drawing_file" string="Zeichnung"/>
    <field name="x_drawing_file"/>
  </xpath>

</data>

```
Source: [snippets/sale.view_order_form.x_drawing_file.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_form.x_drawing_file.xml)

### X Margin Percent  
ID: `mint_system.sale.view_order_form.x_margin_percent`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_form" priority="50">

    <xpath expr="//field[@name='margin']" position="after">
        <field name="x_margin_percent" attrs="{'invisible': [('price_subtotal', '=', 0)]}" optional="hide" widget="percentage"/>
    </xpath>

</data>

```
Source: [snippets/sale.view_order_form.x_margin_percent.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_form.x_margin_percent.xml)

### X Sudio Description  
ID: `mint_system.sale.view_order_form.x_sudio_description`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_form" priority="50">

  <xpath expr="//form[1]/sheet[1]/div[not(@name)][1]/h1[1]/field[@name='name']" position="attributes">
    <attribute name="attrs">{}</attribute>
    <attribute name="readonly"/>
  </xpath>

  <xpath expr="//form[1]/sheet[1]/group[1]" position="after">
    <group name="studio_group_epv6l">
      <group name="studio_group_epv6l_left">
        <field name="x_studio_description" string="Beschreibung"/>
      </group>
    </group>
  </xpath>

</data>

```
Source: [snippets/sale.view_order_form.x_sudio_description.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_form.x_sudio_description.xml)

## View Order Line Tree  
### Fields Optional Hide  
ID: `mint_system.sale.view_order_line_tree.fields_optional_hide`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_line_tree" priority="50">

    <field name="order_id" position="attributes">
        <attribute name="optional">show</attribute>
    </field>
    <field name="order_partner_id" position="attributes">
        <attribute name="optional">show</attribute>
    </field>
    <field name="name" position="attributes">
        <attribute name="optional">show</attribute>
    </field>
    <field name="state" position="attributes">
        <attribute name="optional">hide</attribute>
    </field>
    <field name="salesman_id" position="attributes">
        <attribute name="optional">hide</attribute>
    </field>
    <field name="product_uom_qty" position="attributes">
        <attribute name="optional">hide</attribute>
    </field>
    <field name="qty_delivered" position="attributes">
        <attribute name="optional">hide</attribute>
    </field>
    <field name="qty_invoiced" position="attributes">
        <attribute name="optional">hide</attribute>
    </field>
    <field name="qty_to_invoice" position="attributes">
        <attribute name="optional">hide</attribute>
    </field>
    <field name="product_uom" position="attributes">
        <attribute name="optional">hide</attribute>
    </field>
    <field name="price_subtotal" position="attributes">
        <attribute name="optional">hide</attribute>
    </field>
    <field name="route_id" position="attributes">
        <attribute name="optional">hide</attribute>
    </field>

</data>

```
Source: [snippets/sale.view_order_line_tree.fields_optional_hide.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_line_tree.fields_optional_hide.xml)

### Qty With Sum  
ID: `mint_system.sale.view_order_line_tree.qty_with_sum`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_line_tree" priority="50">

    <field name="product_uom_qty" position="attributes">
        <attribute name="sum">Menge</attribute>
    </field>

    <field name="qty_delivered" position="attributes">
        <attribute name="sum">Gelieferte Menge</attribute>
    </field>

    <field name="qty_invoiced" position="attributes">
        <attribute name="sum">Abgerechnete Menge</attribute>
    </field>

    <field name="qty_to_invoice" position="attributes">
        <attribute name="sum">Abzurechnende Menge</attribute>
    </field>
    
</data>

```
Source: [snippets/sale.view_order_line_tree.qty_with_sum.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_line_tree.qty_with_sum.xml)

### Reset View  
ID: `mint_system.sale.view_order_line_tree.reset_view`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_line_tree" priority="50">

    <field name="order_id" position="after">
        <field name="x_state" />
    </field>

    <field name="name" position="after">
        <field name="product_id" />
    </field>

    <field name="name" position="replace">
    </field>

    <field name="product_id" position="after">
        <field name="blanket_order_line" />
    </field>

    <field name="order_partner_id" position="after">
        <field name="x_client_order_ref" />
    </field>

    <field name="commitment_date" position="after">
        <field name="x_date_order" />
    </field>

    <field name="route_id" position="replace">
    </field>

</data>

```
Source: [snippets/sale.view_order_line_tree.reset_view.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_line_tree.reset_view.xml)

### Show Price Tax  
ID: `mint_system.sale.view_order_line_tree.show_price_tax`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_line_tree" priority="50">

    <field name="price_subtotal" position="before">
        <field name="price_tax"  sum="Gesamtsteuer" optional="show" />
    </field>

</data>

```
Source: [snippets/sale.view_order_line_tree.show_price_tax.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_line_tree.show_price_tax.xml)

### Show Price Unit  
ID: `mint_system.sale.view_order_line_tree.show_price_unit`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_line_tree" priority="50">

    <field name="product_uom_qty" position="after">
        <field name="price_unit" optional="hide"/>
    </field>

</data>

```
Source: [snippets/sale.view_order_line_tree.show_price_unit.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_line_tree.show_price_unit.xml)

### Show Untaxed Amount Invoiced  
ID: `mint_system.sale.view_order_line_tree.show_untaxed_amount_invoiced`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_line_tree" priority="50">

    <field name="price_subtotal" position="after">
        <field name="untaxed_amount_invoiced"  sum="Unversteuerter Rechnungsbetrag" optional="show" />
    </field>

</data>

```
Source: [snippets/sale.view_order_line_tree.show_untaxed_amount_invoiced.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_line_tree.show_untaxed_amount_invoiced.xml)

### X Categ Id  
ID: `mint_system.sale.view_order_line_tree.x_categ_id`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_line_tree" priority="50">

    <field name="name" position="after">
        <field name="x_categ_id" optional="show"/>
    </field>

</data>

```
Source: [snippets/sale.view_order_line_tree.x_categ_id.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_line_tree.x_categ_id.xml)

### X Pricelist Id  
ID: `mint_system.sale.view_order_line_tree.x_pricelist_id`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_line_tree" priority="50">

    <field name="order_partner_id" position="after">
        <field name="x_pricelist_id" optional="show"/>
    </field>

</data>

```
Source: [snippets/sale.view_order_line_tree.x_pricelist_id.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_line_tree.x_pricelist_id.xml)

### X Taxed Amount Invoiced  
ID: `mint_system.sale.view_order_line_tree.x_taxed_amount_invoiced`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_line_tree" priority="50">

    <field name="price_subtotal" position="after">
        <field name="x_taxed_amount_invoiced"  sum="Rechnungsbetrag inkl. MWST" optional="show" />
    </field>

</data>

```
Source: [snippets/sale.view_order_line_tree.x_taxed_amount_invoiced.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_line_tree.x_taxed_amount_invoiced.xml)

### X Weight Delivered  
ID: `mint_system.sale.view_order_line_tree.x_weight_delivered`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_line_tree" priority="50">

    <field name="qty_to_invoice" position="after">
        <field name="x_weight_delivered" sum="Geliefertes Gewicht" optional="show"/>
    </field>

</data>

```
Source: [snippets/sale.view_order_line_tree.x_weight_delivered.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_line_tree.x_weight_delivered.xml)

## View Order Tree  
### Add Carrier  
ID: `mint_system.sale.view_order_tree.add_carrier`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_tree" priority="50">

  <field name="partner_id" position="after">
    <field name="carrier_id" optional="hide"/>
  </field>

</data>

```
Source: [snippets/sale.view_order_tree.add_carrier.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_tree.add_carrier.xml)

### Add Client Order Ref  
ID: `mint_system.sale.view_order_tree.add_client_order_ref`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_tree" priority="50">

  <xpath expr="//field[@name='user_id']" position="before">
      <field name="client_order_ref" optional="show"/>
  </xpath>

</data>
```
Source: [snippets/sale.view_order_tree.add_client_order_ref.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_tree.add_client_order_ref.xml)

### Add Comment  
ID: `mint_system.sale.view_order_tree.add_comment`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_tree" priority="50">

  <xpath expr="//field[@name='user_id']" position="before">
    <field name="comment" optional="show"/>
  </xpath>

</data>
```
Source: [snippets/sale.view_order_tree.add_comment.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_tree.add_comment.xml)

### Show Partner Shipping  
ID: `mint_system.sale.view_order_tree.show_partner_shipping`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_tree" priority="50">

  <field name="partner_id" position="after">
    <field name="partner_shipping_id" optional="hide"/>
  </field>

</data>

```
Source: [snippets/sale.view_order_tree.show_partner_shipping.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_tree.show_partner_shipping.xml)

### Show State  
ID: `mint_system.sale.view_order_tree.show_state`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_tree" priority="50">

  <field name="invoice_status" position="after">
    <field name="state" decoration-success="state == 'sale' or state == 'done'" decoration-info="state == 'draft' or state == 'sent'" widget="badge" optional="show"/>
  </field>

</data>

```
Source: [snippets/sale.view_order_tree.show_state.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_tree.show_state.xml)

### X Product Uom Qty  
ID: `mint_system.sale.view_order_tree.x_product_uom_qty`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_order_tree" priority="50">

  <field name="amount_untaxed" position="before">
    <field name="x_product_uom_qty" sum="Gesamtmenge" optional="hide"/>
  </field>

</data>

```
Source: [snippets/sale.view_order_tree.x_product_uom_qty.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_order_tree.x_product_uom_qty.xml)

## View Quotation Tree  
### Add Client Order Ref  
ID: `mint_system.sale.view_quotation_tree.add_client_order_ref`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_quotation_tree" priority="50">

    <xpath expr="//field[@name='user_id']" position="before">
        <field name="client_order_ref" optional="show"/>
    </xpath>

</data>
```
Source: [snippets/sale.view_quotation_tree.add_client_order_ref.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_quotation_tree.add_client_order_ref.xml)

### Add Comment  
ID: `mint_system.sale.view_quotation_tree.add_comment`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_quotation_tree" priority="50">

    <xpath expr="//field[@name='user_id']" position="before">
        <field name="comment" optional="show"/>
    </xpath>

</data>
```
Source: [snippets/sale.view_quotation_tree.add_comment.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_quotation_tree.add_comment.xml)

### Replace Create Date  
ID: `mint_system.sale.view_quotation_tree.replace_create_date`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_quotation_tree" priority="50">

   <xpath expr="//field[@name='create_date']" position="replace">
        <field name="date_order" widget="date" optional="show"/>
    </xpath>

</data>
```
Source: [snippets/sale.view_quotation_tree.replace_create_date.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_quotation_tree.replace_create_date.xml)

## View Sales Order Filter  
### Add Invoice Status  
ID: `mint_system.sale.view_sales_order_filter.add_invoice_status`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_sales_order_filter" priority="50">

  <xpath expr="//filter[@name='order_month']" position="after">
    <filter string="Status Rechnung" name="state_invoice" domain="[]" context="{'group_by': 'invoice_status'}"/>
  </xpath>

</data>

```
Source: [snippets/sale.view_sales_order_filter.add_invoice_status.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_sales_order_filter.add_invoice_status.xml)

### Add State  
ID: `mint_system.sale.view_sales_order_filter.add_state`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_sales_order_filter" priority="50">

  <xpath expr="//filter[@name='order_month']" position="after">
    <filter string="Status" name="state" domain="[]" context="{'group_by': 'state'}"/>
  </xpath>

</data>

```
Source: [snippets/sale.view_sales_order_filter.add_state.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_sales_order_filter.add_state.xml)

### Modify Order Line  
ID: `mint_system.sale.view_sales_order_filter.modify_order_line`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_sales_order_filter" priority="50">

  <xpath expr="//field[@name='order_line']" position="replace">
    <field name="order_line" string="Product" filter_domain="['|','|',('order_line.product_id', 'ilike', self),('order_line.product_id.type_description', 'ilike', self),('order_line.product_id.type_description2', 'ilike', self)]"/>
  </xpath>

</data>

```
Source: [snippets/sale.view_sales_order_filter.modify_order_line.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_sales_order_filter.modify_order_line.xml)

## View Sales Order Line Filter  
### X Commitment Date  
ID: `mint_system.sale.view_sales_order_line_filter.x_commitment_date`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_sales_order_line_filter" priority="50">

  <filter name="to_invoice" position="after">
    <filter string="Liefertermin" name="date_commitment" date="x_commitment_date" />
  </filter>
  
</data>
```
Source: [snippets/sale.view_sales_order_line_filter.x_commitment_date.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_sales_order_line_filter.x_commitment_date.xml)

### X Date Order  
ID: `mint_system.sale.view_sales_order_line_filter.x_date_order`  
```xml
<?xml version="1.0"?>
<data inherit_id="sale.view_sales_order_line_filter" priority="50">

  <filter name="to_invoice" position="after">
    <separator/>
    <filter string="Auftragsdatum" name="date_order" date="x_date_order" />
  </filter>
  
</data>
```
Source: [snippets/sale.view_sales_order_line_filter.x_date_order.xml](https://github.com/Mint-System/Odoo-Development/tree/14.0/snippets/sale.view_sales_order_line_filter.x_date_order.xml)

