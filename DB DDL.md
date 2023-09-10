![Untitled6](https://github.com/DenisPankiv/DBDesing/assets/78309206/caf33c13-c138-450e-b4cb-c69c1fd74192)

CREATE TABLE [Agent] (
	AgentID int NOT NULL,
	FullName varchar(30) NOT NULL,
	Adress varchar(30) NOT NULL,
	City varchar(20) NOT NULL,
	PhoneNumber int NOT NULL,
	Email varchar(30) NOT NULL,
  CONSTRAINT [PK_AGENT] PRIMARY KEY CLUSTERED
  (
  [AgentID] ASC
  ) WITH (IGNORE_DUP_KEY = OFF)

)
GO
CREATE TABLE [Client] (
	ClientID int NOT NULL,
	FullName varchar(30) NOT NULL,
	Adress varchar(30) NOT NULL,
	City varchar(20) NOT NULL,
	PhoneNumber int NOT NULL,
	Email varchar(30) NOT NULL,
  CONSTRAINT [PK_CLIENT] PRIMARY KEY CLUSTERED
  (
  [ClientID] ASC
  ) WITH (IGNORE_DUP_KEY = OFF)

)
GO
CREATE TABLE [Reports] (
	ReportID int NOT NULL,
	AgentID int NOT NULL,
	ManagerID int NOT NULL,
	ReportName varchar(30) NOT NULL,
	ReportDate datetime NOT NULL,
	Description varchar(100),
	Comission money,
  CONSTRAINT [PK_REPORTS] PRIMARY KEY CLUSTERED
  (
  [ReportID] ASC
  ) WITH (IGNORE_DUP_KEY = OFF)

)
GO
CREATE TABLE [Contacts] (
	ContactID int NOT NULL,
	InsuranceID int NOT NULL,
	AgentID int NOT NULL,
	ClientID int NOT NULL,
	ClientFullName varchar(30) NOT NULL,
  CONSTRAINT [PK_CONTACTS] PRIMARY KEY CLUSTERED
  (
  [ContactID] ASC
  ) WITH (IGNORE_DUP_KEY = OFF)

)
GO
CREATE TABLE [Manager] (
	ManagerID int NOT NULL,
	ManagerName varchar(30) NOT NULL,
	AgentID int NOT NULL,
	ReportsID int NOT NULL,
  CONSTRAINT [PK_MANAGER] PRIMARY KEY CLUSTERED
  (
  [ManagerID] ASC
  ) WITH (IGNORE_DUP_KEY = OFF)

)
GO
CREATE TABLE [InsuranceContract] (
	InsuranseContractID int NOT NULL,
	InsuranceType varchar(20) NOT NULL,
	ClientID int NOT NULL,
	ContractAmount money NOT NULL,
	AgentID int NOT NULL,
	ValidityStart datetime NOT NULL,
	ValidityEnd datetime NOT NULL,
	Price money NOT NULL,
	Discount float,
  CONSTRAINT [PK_INSURANCECONTRACT] PRIMARY KEY CLUSTERED
  (
  [InsuranseContractID] ASC
  ) WITH (IGNORE_DUP_KEY = OFF)

)
GO


ALTER TABLE [Reports] WITH CHECK ADD CONSTRAINT [Reports_fk0] FOREIGN KEY ([ManagerID]) REFERENCES [Manager]([ManagerID])
ON UPDATE CASCADE
GO
ALTER TABLE [Reports] CHECK CONSTRAINT [Reports_fk0]
GO

ALTER TABLE [Contacts] WITH CHECK ADD CONSTRAINT [Contacts_fk0] FOREIGN KEY ([AgentID]) REFERENCES [Agent]([AgentID])
ON UPDATE CASCADE
GO
ALTER TABLE [Contacts] CHECK CONSTRAINT [Contacts_fk0]
GO
ALTER TABLE [Contacts] WITH CHECK ADD CONSTRAINT [Contacts_fk1] FOREIGN KEY ([ClientID]) REFERENCES [Client]([ClientID])
ON UPDATE CASCADE
GO
ALTER TABLE [Contacts] CHECK CONSTRAINT [Contacts_fk1]
GO

ALTER TABLE [Manager] WITH CHECK ADD CONSTRAINT [Manager_fk0] FOREIGN KEY ([AgentID]) REFERENCES [Agent]([AgentID])
ON UPDATE CASCADE
GO
ALTER TABLE [Manager] CHECK CONSTRAINT [Manager_fk0]
GO

ALTER TABLE [InsuranceContract] WITH CHECK ADD CONSTRAINT [InsuranceContract_fk0] FOREIGN KEY ([ClientID]) REFERENCES [Client]([ClientID])
ON UPDATE CASCADE
GO
ALTER TABLE [InsuranceContract] CHECK CONSTRAINT [InsuranceContract_fk0]
GO
ALTER TABLE [InsuranceContract] WITH CHECK ADD CONSTRAINT [InsuranceContract_fk1] FOREIGN KEY ([AgentID]) REFERENCES [Agent]([AgentID])
ON UPDATE CASCADE
GO
ALTER TABLE [InsuranceContract] CHECK CONSTRAINT [InsuranceContract_fk1]
GO

