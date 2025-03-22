# React Components Guide

## Editor
```tsx
const [editorContent, setEditorContent] = useState('');
const handleEditorChange = (content: any) => {
  setEditorContent(content);
};

<QuillEditorReact
  value={editorContent}
  onChange={handleEditorChange}
/>
```

---

## Loader
```tsx
import Loader from "../../../Components/Loader";
const [isLoadingStatus, setIsLoadingStatus] = useState(false);

<Loader isLoading={isLoadingStatus} className="text-center" />

<Col xs={12} md={12} className="rightSide">
  <Loader isLoading={loading} className="text-center" />
</Col>
```

---

## Toast Notifications
```tsx
const toastId = toast.loading('Loading...', { position: 'top-right' });
toast.dismiss(toastId);

toast.success('Login Success', { duration: 2000, position: 'top-right' });
toast.error(item?.message || 'An error occurred during login.', { duration: 4000, position: 'top-right' });
```

---

## Common Search Function on Button
```tsx
const handleSearchFuncApi = async () => {
  let obj = {
    module: "PO",
    queryName: "getMaterialPO",
    page: 1,
    per_page: 10,
    searchTerm: getCommonSearchTxt,
  };
  dispatch(getPurchaseOrder(obj));
};

<SearchField
  name="searchKey"
  value={getCommonSearchTxt}
  onChange={(event) => setCommonSearchTxt(event.target.value)}
  onClick={() => handleSearchFuncApi()}
/>
```

---

## Combobox Field
```tsx
<ComboboxField
  label="Tech Focal Point"
  data={getTechnicalUserList}
  id="rfxTechFocalPersonId"
  name="rfxTechFocalPersonId"
  setValue={formInputs.rfxTechFocalPersonId || ""}
  getvalue={setDropdownData}
/>

const [getDropdownData, setDropdownData] = useState([]);

useEffect(() => {
  setFormInputs((formInputs) => ({
    ...formInputs,
    [getDropdownData?.textField]: getDropdownData?.selected,
  }));
}, [getDropdownData]);
```

---

## Input Field
```tsx
<InputField
  id="documentDate"
  className="inputBox"
  label="Document Date"
  name="documentDate"
  type="date"
  value={formInputs.documentDate}
  onChange={onInputChange}
  disabled={getDisabledStatus}
/>
```

```tsx
const onInputChange = ({ target: { name, value } }) => {
  setFormInputs((formInputs) => ({ ...formInputs, [name]: value }));
};
```

---

## Multiselect Field
```tsx
<MultiselectField
  label="Roles"
  placeholder="Please select the Roles"
  data={getRoleIdVal}
  id="roles"
  getvalue={setDropdownData}
  className="dropdownOption"
  disabled={true}
  setValue={getRoleIdText}
/>
```

---

## Common Redux Configuration
```tsx
import { useSelector } from "react-redux";
const appConfig = useSelector((state) => state?.app?.appConfig);
```

```tsx
{appConfig?.productLogo}
{appConfig?.customerLogo1}
{appConfig?.productTitle}
{appConfig?.customerName}
```

---

## DataTable: User Role Column Restrictions
```tsx
useEffect(() => {
  const userRole = userData?.roles?.[0]?.roleId || null;
  const restrictedColumns = {
    "SALES-MANAGER": ["Process"],
    "SALES-OFFICER": ["Process"],
  };

  const filteredCol = userListColInfo.filter(
    (col) => !restrictedColumns[userRole]?.includes(col.name)
  );
  setFilteredUserListColInfo(filteredCol);
}, [userData]);
```

---

## File Upload Component
```tsx
import FileUploadComponent from "../../../../Components/formElements/FileUploadComponent";

const onSuccessUploadDocumentType = (data) => {
  setFormInputs((formInputs) => ({
    ...formInputs,
    [data.fieldName]: data.attachmentId,
  }));
};

<FileUploadComponent
  id="purchaseOrderFileAttachment"
  name="purchaseOrderFileAttachment"
  label="Customer PO"
  allowedTypes={["image/png", "image/jpeg", "application/pdf"]}
  multiple={true}
  required={true}
  onSuccessUpload={onSuccessUploadDocumentType}
  value={formInputs.ISOCertification || ""}
/>
```

---

## File Viewer Modal
```tsx
import FileViewerModal from "../../../../Components/FileViewer/FileViewerModal";

const [getShowFileViewModal, setShowFileViewModal] = useState(false);
const [getFileViewData, setFileViewData] = useState(null);

const handleViewFile = (fileAttachmentId) => {
  setFileViewData(fileAttachmentId);
  setShowFileViewModal(true);
};
```

```tsx
<FileViewerModal
  show={getShowFileViewModal}
  onHide={handleViewFileHide}
  fileid={getFileViewData}
/>
```

---

## Data Table Dropdown Menu
```tsx
import TableDropdownMenu from "../../../../Components/TableDropdownMenu/TableDropdownMenu";
```

```tsx
const handleDropdownChange = (data) => {
  setProductDetailsData((prevRows) =>
    prevRows.map((row) =>
      row.local_id === data.index ? { ...row, [data.name]: data.value } : row
    )
  );
};
```

```tsx
{
  name: "Royality Name",
  cell: (row) => (
    <TableDropdownMenu
      index={row.local_id}
      label={"Royality Name"}
      data={royalityNameData}
      id={"royalityName"}
      name={"royalityName"}
      onChange={handleDropdownChange}
    />
  ),
  sortable: true,
  width: "200px",
}
```

---

## UI Visibility Based on Roles
```tsx
import { hasAccess } from "../../../../utils/roleUtils";
const userRole = useSelector((state) => state?.user?.data?.roles?.[0]?.roleId);

{hasAccess(userRole, "buttons", "customer_details_edit", pageConfigInfo) && (
  <Col xs={6} md={2} lg={2} className="text-left">
    <button className="btnInfo" onClick={editCustomer}>Edit</button>
  </Col>
)}
```

