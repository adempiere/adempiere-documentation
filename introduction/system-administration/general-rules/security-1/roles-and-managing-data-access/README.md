# Roles and Managing Data Access

## User Level

The user level determines the extent of information the User has access to. The possible settings and limitations are shown in the table below. Organization access is controlled via the fields _**Access All Orgs**_, _**Use User Org Access**_ and through the **Org Access** tab in the **Role** window. Table access levels are set by the System Administrator but can be further restricted by Role in the **Role Data Access** window.

{% hint style="info" %}
Organizations are specified by name except for a special organization identified by the asterisk symbol \(\*\) which means All Organizations.
{% endhint %}

<table>
  <thead>
    <tr>
      <th style="text-align:left">Users with this Level...</th>
      <th style="text-align:left">Can update records from the ...</th>
      <th style="text-align:left">and can view tables with Access Level ...</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Client</td>
      <td style="text-align:left">Login Client and all Organizations (*)</td>
      <td style="text-align:left">All,
        <br />Client Only,
        <br />Client + Organization,
        <br />System + Client</td>
    </tr>
    <tr>
      <td style="text-align:left">Client + Organization</td>
      <td style="text-align:left">Login Client and all allowed Organizations, including *</td>
      <td style="text-align:left">
        <p>All,
          <br />Client Only,
          <br />Organization,
          <br />Client + Organization</p>
        <p>System + Client</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Organization</td>
      <td style="text-align:left">Login Client and all allowed Organizations except *</td>
      <td style="text-align:left">
        <p>All,</p>
        <p>Organization,
          <br />Client + Organization</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">System</td>
      <td style="text-align:left">System Client and Organization *</td>
      <td style="text-align:left">All,
        <br />System Only,
        <br />System + Client</td>
    </tr>
  </tbody>
</table>

