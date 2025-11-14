# ChemCOG

Welcome to ChemCOG. This is a small project that I made to allow chemists to perform lookups in Excel for common materials. It uses the [MolPort API](https://www.molport.com/shop/api) and the [PubChem PUG REST API](https://pubchem.ncbi.nlm.nih.gov/docs/pug-rest) to allow programmatic lookups via some short VBA scripts. 

This allows you to perform a batch lookup if you want to get information on a number of molecules (starting materials, reagents, catalysts, etc.) and quickly find the cheapest large quantity that is available on MolPort.

## What ChemCOG Can Do

ChemCOG will allow you to do the following:

1. Use a name or synonym to find a SMILES string or vice versa
2. Use a SMILES string to lookup the CAS number, molecular weight, and MolPort ID number (providing a link to the compound's MolPort page)
3. Find vendor, quantity, price, and lead time information for the chemical in question on MolPort

## What Is Requires

In order to use ChemCOG, you have to have a MolPort user account and an API key. These are free to obtain. The [MolPort Chemical Search API](https://www.molport.com/shop/api-documentation-v-3-0) allows each user to perform 10 000 searches per month with their API key.

## How to Use It

### ChemID Lookups

If you just want to search for SMILES, CAS, MW, and names of compounds, you can use the following functions which are built into the workbook:

 - =getCASFromSMILES()
 - getNameFromSMILES()
 - getSMILESFromName()
 - getMolWtFromSMILES

These query the PUG REST API to obtain the data above. Obtaining the SMILES string is critical if you want to look up 

### COG Table

1. Download the Excel file.
2. Press Alt+F11 to open the Visual Basic Editor. Under the Excel workbook's "Modules" double click "MolPortLookup".
3. At the top of the script, fill in the MOLPORT_API_KEY, MOLPORT_USERNAME, and MOLPORT_PASSWORD.
4. In the table, enter the name of the compound you want to search for in the "Raw Material" column.
5. Press the "Calculate All" button to obtain the SMILES, CAS, and MW for each name you entered.
6. Press the "Retrieve Supplier..." button to query the MolPort API and fill in your table automatically.

This also includes a link to the MolPort page for each chemical in question. If you click the entry under "MolPort ID" it will take you to the page where you can look at other suppliers, quantities, etc. for the material.

The COG lookup is set to give you the sourcing information for the **largest** available delivery size. This is because it was written by a process chemist, and I don't deal in milligram or single gram quantities often. For extremely common materials, it will not be unusual for you to find pack sizes in the tens of kilograms. However, if for a rare molecule the highest available pack size is only 5 g, it will still give you that (albeit converted to kg units!).

The table then also calculates the $/kg and $/mol for the materials in question.

## Before Using

Please note that this tool is not perfect. It is recommended that you use the most common name to search for each material.

If you are looking for a specific **preparation** of a material (for instance, a solution of trimethylaluminum in toluene, as opposed to pure trimethylaluminum) this will not work very well, because the SMILES string will not be different, nor will the CAS. 

The compound must exist in the PubChem database to be searchable! It is true that not every commercially available compound is in PubChem, and not every compound in PubChem is commercially available.

That said, it works fairly well if you want to get approximate costs without going to considerable effort or engaging a commercial sourcing specialist.

Enjoy.
