# Control System Studio RAP products

Repository contains products definitions for the CS-Studio RAP products. It includes:  
- Web OPI: BOY runner (org.csstudio.opibuilder.rap.product)  
- Web Data Browser: Archive viewer based on BEAUtY (org.csstudio.trends.databrowser2.rap.product)  
- Web Alarm: BEAST Alarm Viewer (org.csstudio.alarm.beast.ui.rap.product)  

All products depend on the [cs-studio](https://github.com/ControlSystemStudio/cs-studio). In order to build the war products you need to provide a p2 repository that contains all plugins. By default it will try to fetch them from the [css update site](http://download.controlsystemstudio.org/updates/<ver>). If you want to use cs-studio plugins that are newer than the on on the p2 repository, make sure that they are available in your local p2 or maven repository.  

To build the RAP products execute command **mvn clean verify**. If the operation was completed successfully the war products will be located in the **wars** folder.  

# Notes  

All three products are feature based products, which means that if you need to add an additional plugin, you first have to create a feature that contains that plugin. Doing so, make sure that your feature contains only the plugins that you need and nothing else; every additional plugin increases the final product size and causes it to start more slowly. If you can't get around that, at least make sure that all plugins that are included in the feature are RAP compatible. In addition, it is highly recommended that all your features are added directly to the product file - none of the features should include any additional feature, though it may depend on other features.  

Do not forget that every plugin that is included in your final product needs to have the **autoStart=true** (this is the reason why you do not want to have unnecessary plugins in your product). After you add an additional feature to the product configuration file, you have to open the **Configuration** tab of your product file, add the new plugins to the start levels list, and change their Auto-Start values (this is not required for fragments, which are automatically started if their host is started).  

The existing databrowser product includes only the BEAUtY reader plugin. If you need access to other archivers, you have to prepare a feature that includes all required plugins and then add that feature to the existing product.  

The web opi includes the core widgets and the databrowser widget. If you want to add additional widgets, make sure that the widgets are RAP compatible. For example, **alarmtable.opiwidget** is already RAP compatible, but **..opibuilder.widgets.extra** is not.  
