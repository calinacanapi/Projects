-- LOOKING AT OUR DATA FIRST

SELECT *
 FROM `portfolioproject-377323.PortfolioProject1.NashvilleHousing` 

 -- CLEANING DATA IN SQL QUERIES
 --STANDARDIZE DATE FROM DATETIME TO DATE


SELECT SaleDateConverted, CONVERT(Date,SaleDate)
FROM `portfolioproject-377323.PortfolioProject1.NashvilleHousing`

UPDATE NashvilleHousing
SET SaleDate = CONVERT(Date,SaleDate)
--Populate Property Address Data

SELECT *
FROM `portfolioproject-377323.PortfolioProject1.NashvilleHousing`
--WHERE PropertyAddress IS NULL
ORDER BY ParcelID

SELECT a.ParcelID, a.PropertyAddress, b.ParcelID, b.PropertyAddress, IFNULL(a.PropertyAddress, b.PropertyAddress)
FROM `portfolioproject-377323.PortfolioProject1.NashvilleHousing` as a
JOIN `portfolioproject-377323.PortfolioProject1.NashvilleHousing` as b 
ON a.ParcelID = b.ParcelID
AND a.[UniqueID_] <> b.[UniqueID_]
WHERE a.PropertyAddress IS NULL

UPDATE a
SET PropertyAddress = IFNULL(a.PropertyAddress, b.PropertyAddress)
FROM `portfolioproject-377323.PortfolioProject1.NashvilleHousing` a
JOIN `portfolioproject-377323.PortfolioProject1.NashvilleHousing` b
ON a.ParcelID = b.ParcelID
AND a.[UniqueID_] <> [b.UniqueID_]
WHERE a.PropertyAddress IS NULL

--Breaking Addresses into Individual Columns (Address, City, State)

SELECT PropertyAddress
FROM `portfolioproject-377323.PortfolioProject1.NashvilleHousing`

SELECT
SUBSTRING(PropertyAddress,1,CHARINDEX(',', PropertyAddress -1)) as Address,
SUBSTRING(PropertyAddress,1,CHARINDEX(',', PropertyAddress +1)),LEN(PropertyAddress)) AS Address
FROM  `portfolioproject-377323.PortfolioProject1.NashvilleHousing`

ALTER TABLE NashvilleHousing
ADD PropertySplitAddress Nvarchar(255);

UPDATE NashvilleHousing
SET PropertySplitAddress = SUBSTRING(PropertyAddress,1,CHARINDEX(',',PropertyAddress)-1)

ALTER TABLE NashvilleHousing
ADD PropertySplitCity Nvarchar(255)

UPDATE NashvilleHousing
SET PropertySplitCity = SUBSTRING(PropertyAddress,CHARINDEX(',',PropertyAddress)+1, LEN(PropertyAddress)))
SELECT *
FROM `portfolioproject-377323.PortfolioProject1.NashvilleHousing`



SELECT OwnerAddress
FROM `portfolioproject-377323.PortfolioProject1.NashvilleHousing`

--Use Parse Name 
SELECT
PARSENAME(REPLACE(OwnerAddress,',''.',3)
PARSENAME(REPLACE(OwnerAddress,',''.',2)
PARSENAME(REPLACE(OwnerAddress,',''.',1)
FROM `portfolioproject-377323.PortfolioProject1.NashvilleHousing`


ALTER TABLE NashvilleHousing
ADD OwnerSplitAddress Nvarchar(255);

UPDATE NashvilleHousing 
SET OwnerSplitAddress = PARSENAME(REPLACE(OwnerAddress,',''.',3)

ALTER TABLE NashvilleHousing
ADD OwnerSplitCity Nvarchar(255);

UPDATE NashvilleHousing
SET OwnerSplitCity = PARSENAME(REPLACE(OwnerAddress,',''.',2)

ALTER TABLE NashvilleHousing
ADD OwnerSplitState Nvarchar(255);

UPDATE NashvilleHousing
SET OwnerSplitState = PARSENAME(REPLACE(OwnerAddress,',''.',1)

SELECT * 
FROM `portfolioproject-377323.PortfolioProject1.NashvilleHousing`

--Change Y and N to Yes and No

SELECT SoldAsVacant,
CASE WHEN SoldAsVacant = 'Y' THEN 'Yes'
     WHEN SoldAsVacant = 'N' THEN 'No'
     ELSE SoldAsVacant
     END
FROM `portfolioproject-377323.PortfolioProject1.NashvilleHousing`


UPDATE NashvilleHousing
SET SoldAsVacant = 
CASE WHEN SoldAsVacant = 'Y' THEN 'Yes'
     WHEN SoldAsVacant = 'N' THEN 'No'
     ELSE SoldAsVacant
     END
FROM `portfolioproject-377323.PortfolioProject1.NashvilleHousing`

--REMOVE DUPLICATES USING A CTE

WITH RowNumCTE AS(
SELECT *, 
 ROW_NUMBER() OVER (
   PARTITION BY ParcelID,
                PropertyAddress,
                SalePrice,
                SaleDate,
                LegalReference
                ORDER BY 
                  UniqueID_
 ) row_num
FROM `portfolioproject-377323.PortfolioProject1.NashvilleHousing`
--ORDER BY ParcelID
)
DELETE 
FROM RowNumCTE
WHERE row_num > 1
--ORDER BY PropertyAddress



--DELETE UNUSED COLUMNS
SELECT *
FROM `portfolioproject-377323.PortfolioProject1.NashvilleHousing`

ALTER TABLE `portfolioproject-377323.PortfolioProject1.NashvilleHousing`
DROP COLUMN OwnerAddress, TaxDistrict, PropertyAddress
ALTER TABLE `portfolioproject-377323.PortfolioProject1.NashvilleHousing`
DROP COLUMN SaleDate
