<img src="images/axiad_logo.png" align="center">
 

# Axiad

Axiad enables customers to move to a passwordless future without the friction and risk of fragmented solutions. By addressing authentication holistically, regardless of underlying IT complexity, organizations can vastly improve their cybersecurity posture.

Please refer to our website for more information about [Axiad](https://www.axiad.com/).

## Axiad SCIM Connector

Axiad SCIM Connector enables automatic provisioning of users and groups between Axiad Cloud and ForgeRock using the secure and standard protocol, System for Cross-Domain Identity Management(SCIM). The Axiad SCIM connector allows partners to leverage certificate based authentication, which is the most secure, phishing-resistant form of multi-factor authentication (MFA) and is being increasingly deployed in enterprises as well as the public sector. Many enterprise employees, as well as the majority of federal agencies and defense employees/contractors, use a strong authenticator such as a smart card or hardware device for authentication. CBA streamlines the process of authenticating users with a variety of authenticators while improving overall protection.

Axiad provides this SCIM Connector as a starting point for integrating ForgeRock and Axiad Cloud. Since every ForgeRock implementation is different we have provided a basic mapping of ForgeRock attributes for SCIM provisioning. Your organization's implementation may have differences which will require updates to ensure the SCIM Connector works properly.

Your Axiad SCIM Connector may also not require all the attributes that are described below or your ForgeRock implementation may not have all the data populated for all attributes listed. The SCIM attribute mapping will need to be updated as appropriate for your data and business requirements. 

Please work with [Axiad Customer Success](mailto:customer.success@axiad.com) before implementing a SCIM connector as they will need to provide an attribute list and credentials for your Axiad Cloud tenant.

## Prerequisites

1. ForgeRock Identity Management (OpenIDM) 7.3.0 or above
1. Axiad Cloud tenant
1. Axiad Cloud tenant available attribute list
1. Axiad Cloud tenant SCIM credentials
1. Appropriate Axiad SCIM connector configuration files

## Axiad Configuration

If your Axiad Cloud tenant is already configured with the required mappings attribute there is no additional Axiad configuration needed. If assistance is needed with your Axiad Cloud environment in the following sections please contact [Axiad Customer Success](mailto:customer.success@axiad.com).

## Configuring the Axiad SCIM Connector

1. Get the latest SCIM Connector configuration and mapping file from the [Axiad Customer Success](mailto:customer.success@axiad.com) team.
2. Copy the `provisioner.openicf-AxiadSCIMConnector.json` file into the `conf` directory where ForgeRock Identity Management is deployed.
3. If the `sync.json` file exist into `conf` directory, copy the contents of `mapping-AxiadSCIMConnector.json` in the mappings array inside the `conf\sync.json` file. If the `sync.json` file doesn't exist, copy the sync.json file in the `conf` directory.

## ForgeRock Configuration

### 1. Axiad SCIM Connector Configuration

1. Log into the ForgeRock Identity Management console
2. Click `CONFIGURE` on the menu bar and select `CONNECTORS`. AxiadSCIMConnector will be available as shown
  
   ![Axiad SCIM Connector |10x10](./images/axiad_scim_connector.png)

3. Click on the `Axiad SCIM Connector`

   3.1. Configure the `SCIM Endpoint` under `Base Connector Details` section as shown. If you do not have the SCIM endpoint please contact [Axiad Customer Success](mailto:customer.success@axiad.com)
  
   ![SCIM Endpoint](./images/scim_endpoint_config.png)

   3.2. Configure the `Authentication token` under the `Additional Options` section as shown. If you do not have the token please contact [Axiad Customer Success](mailto:customer.success@axiad.com)
  
   ![Authentication Token](./images/authentication_token_config.png)

   3.3. Click on save.

### 2. Axiad SCIM Connector mappings Configuration   
   Click `CONFIGURE` on the menu bar and select `Mappings`. Axiad SCIM mappings will be available as shown
  
   ![Axiad SCIM Mappings](./images/axiad_scim_mappings.png)

#### _2.1. User mapping Configurations_

1. Click on `Edit` where SOURCE is `Managed/User` and verify the settings are correct. You should have received a list of supported SCIM attributes from the Axiad Customer Success team. The attribute list Axiad provides includes all attributes mapped within your Axiad Cloud tenant. You must delete all unused attributes from the SCIM mapping to avoid unnecessary data synchronizations.

   1.1. Verify the `Properties` tab has the `Attributes Grid` as shown
  
      ![User_properties_tab](./images/users_mapping/user_properties_tab.png)

   **_Note_** : By default the `Organization` property is mapping to the 1st organization in an array. If this is different than what you expect please change the mapping accordingly.

   1.2. Verify the `Association` tab has the `Association Rules` as shown
  
      ![User_association_tab](./images/users_mapping/user_association_tab.png)

      1.2.1. Under `Association Rules` click on the `pencil` icon (as highlighted in above image) to verify the `Correlation Query` config as shown
  
      ![User_correlation_query](./images/users_mapping/user_correlation_query.png)

   1.3. Verify the `Behaviors` tab has the `Policies` as shown
  
      ![User_behaviors_tab](./images/users_mapping/user_behaviors_tab.png)

   1.4. Verify the `Advanced` tab has the `Additional Mapping Options` as shown 
  
      ![User_advanced_tab](./images/users_mapping/user_advanced_tab.png)  
       
   1.5. Under the `Scheduling` tab, you can `Add Reconciliation Schedule` as per your organization's requirements

#### _2.2. Group mapping Configurations_

1. Click on `Edit` where SOURCE is `Managed/Role` and verify the settings are correct

   1.1. Verify the `Properties` tab has the `Attributes Grid` as shown
  
      ![User_properties_tab](./images/groups_mapping/group_properties_tab.png)

   1.2. Verify the `Association` tab has the `Association Rules` as shown
  
      ![User_association_tab](./images/groups_mapping/group_association_tab.png)

      1.2.1. Under `Association Rules` click on the `pencil` icon (as highlighted in above image) to verify the `Correlation Query` config as shown
  
      ![User_correlation_query](./images/groups_mapping/group_correlation_query.png)

   1.3. Verify the `Behaviors` tab has the `Policies` as shown
  
      ![User_behaviors_tab](./images/groups_mapping/group_behaviors_tab.png)

   1.4. Verify the `Advanced` tab has the `Additional Mapping Options` as shown 
  
      ![User_advanced_tab](./images/groups_mapping/group_advanced_tab.png)  
       
   1.5. Under the `Scheduling` tab, you can `Add Reconciliation Schedule` as per your organization's requirements

### _2.3. Managed Objects Configuration_

#### 1. Users

1. Click `CONFIGURE` on the menu bar and select `MANAGED OBJECTS`
2. Click the 'User' managed object

##### 1.1. Manager property

1. Edit the `manager` property 
2. Under `Details`, click on `Show advanced options`
3. Enable `Viewable`, `User Editable`, `Return by Default` and the `Notify Self` options as shown

   ![Manager_property_options](./images/users_mapping/manager_property_options.png)

4. Edit the `Relationship Configuration`, highlighted with a red rectangle as shown

    ![Manager_edit_relationship](./images/users_mapping/manager_edit_relationship.png)

   4.1. Enable `Notify` on the `Edit Resource` screen as shown

      ![Edit_resource](./images/users_mapping/edit_resource.png)

##### 1.2. MemberOfOrgIDs property

1. Edit the `memberOfOrgIDs` property
2. Under `Details`, click on `Show advanced options`
3. Enable `User Editable`, `Return by Default` and the `Virtual` options as shown

    ![MemberOfOrgIDs_property_option](./images/users_mapping/memberOfOrgIDs_property_option.png)

#### 2. Roles

1. Click `CONFIGURE` on the menu bar and select `MANAGED OBJECTS`
2. Click the 'Role' managed object

##### 2.1. Members property

1. Edit the `members` property 
2. Under `Details`, click on `Show advanced options`
3. Enable `Viewable`, `User Editable`, `Return by Default` and the `Notify Self` options as shown

   ![Members_property_options](./images/groups_mapping/members_property_options.png)
 
4. Edit the `Relationship Configuration`, highlighted with a red rectangle as shown

    ![Member_edit_relationship](./images/groups_mapping/member_edit_relationship.png)

   4.1. Enable `Notify` on the `Edit Resource` screen as shown

      ![Edit_resource](./images/groups_mapping/edit_resource.png)

## Post configuration steps

1. Test `User` provisioning by creating a user in ForgeRock and making sure it is provisioned in the Axiad Cloud and all the mappings are working as expected.
2. Test `Role` provisioning by creating a role in ForgeRock and making sure it is provisioned in the Axiad Cloud and all the mappings are working as expected.

