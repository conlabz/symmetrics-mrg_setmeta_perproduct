* DOCUMENTATION

** INSTALLATION
Extrahieren Sie den Inhalt dieses Archivs in Ihr Magento Verzeichnis. Die Verzeichnisstruktur ist bereits auf die des Magentoverzeichnisses angepasst.
Auch die ben�tigte Konfigurationsdatei um das Modul zu aktivieren ist bereits in diesem Archiv enthalten.
Ggf. ist das Leeren/Auffrischen des Magento-Caches notwendig.

** USAGE
Dieses Modul f�llt die Meta-Daten eines Produktes automatisch mit dem Produktnamen und den Kategorien.

** FUNCTIONALITY
*** A:	Wenn die Felder mit den Meta-Informationen leer sind, lese per Javascript den Produktnamen und die Kategorien aus und trage ihn in die entsprechenden Felder ein.

** TECHNINCAL
Die Meta Informationen und der Produktname stehen im Quelltext auf der gleichen Seite, deswegen kann das Input Feld einfach ausgelesen werden. Die Kategorien hingegen werden mit Ajax von einem eigenen Controller "Symmetrics_SetMeta_Admin_SetmetaController" im JSON Format geholt und in eine Komma-Seperierte Liste gepackt.
Dieser Controller bezieht die Daten aus einem eigenen Model "Symmetrics_SetMeta_Model_SetMeta". Der Block "Symmetrics_SetMeta_Block_Catalog_Product_Edit" musste �berschrieben werden, um die Javascript Funktionen bei den Speicherbuttons einzuklinken.

** PROBLEMS
Wenn sich Produktname oder Kategorien �ndern, werden die Meta Informationen nicht geupdated, weil das Modul pr�ft, ob die Felder leer sind und nur dann reagiert. Ansonsten w�rden manuell angelegte Informationen �berschrieben werden.

* TESTCASES

** BASIC
*** A:	1. Installieren Sie das Modul.
	2. Legen Sie im Backend �ber Catalog->Add Product ein neues Produkt an.
	3. Geben Sie wenigstens die ben�tigten Attribute und eine Kategorie an
	4. W�hlen Sie "Save & Continue Edit".
	5. Die Meta-Felder sollten nun mir den Kategorie und Namensinformationen gef�llt werden.