# Agent

## Classes

### `Agent`

A person or group or organization with economic agency.

## Queries

### `myAgent`
Loads details of the currently authenticated REA agent
> Status: Implemented

### `agent`
Find an agent (person or organization) by their ID
> Status: Implemented

### `organization`
Find an organization (group) agent by its ID
> Status: Implemented

### `person`
Find a person by their ID
> Status: Implemented

### `agents`
Loads all agents publicly registered within this collaboration space
> Status: Implemented

### `organizations`
Loads all organizations publicly registered within this collaboration space
> Status: Implemented

### `people`
Loads all people who have publicly registered with this collaboration space.
> Status: Implemented

### `agentRelationship`
Retrieve details of an agent relationship by its ID
> Status: Unimplemented

### `agentRelationships`
Retrieve details of all the relationships between all agents registered in this collaboration space
> Status: Unimplemented

### `agentRelationshipRole`
Retrieve details of an agent relationship role by its ID
> Status: Unimplemented

### `agentRelationshipRoles`
Retrieve all possible kinds of associations that agents may have with one another in this collaboration space
> Status: Unimplemented

## Mutations

### `associateMyAgent`
Associates the Agent identified by agentId with the currently authenticated user. Can only be used once.
> Status: Implemented

### `createPerson`
Registers a new (human) person with the collaboration space
> Status: Implemented

### `updatePerson`
Update profile details
> Status: Implemented

### `deletePerson`
Erase record of a person and thus remove them from the collaboration space
> Status: Implemented

### `createOrganization`
Registers a new organization (group agent) with the collaboration space
> Status: Implemented

### `updateOrganization`
Update organization profile details
> Status: Implemented

### `deleteOrganization`
Erase record of an organization and thus remove it from the collaboration space
> Status: Implemented

### `createAgentRelationship`

> Status: Unimplemented

### `updateAgentRelationship`

> Status: Unimplemented

### `deleteAgentRelationship`

> Status: Unimplemented

### `createAgentRelationshipRole`

> Status: Unimplemented

### `updateAgentRelationshipRole`

> Status: Unimplemented

### `deleteAgentRelationshipRole`

> Status: Unimplemented

