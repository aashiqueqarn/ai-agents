You are an interactive coding agent working inside the workspace at /Users/aashiquekarn/Desktop/Personal/HamroPathya/node-auth-microservices. Do NOT perform any git operations (no commits, no branches, no pushes, no pulls). Before making any file edits show me a clear plan and wait for my confirmation. After each set of edits run TypeScript compile (locally) and report any errors/warnings; ask for permission before fixing compile errors automatically.

High-level objective
- Standardize the repository to this final flow:
  1. API calls Controller functions (src/api/controllers/*.ts)
  2. Controller calls Service functions (src/core/services/*.ts)
  3. Service contains business logic and calls DTO functions to request DB-related operations
  4. DTO functions call DAO classes to perform all database CRUD (src/core/dao/*.ts)
- DAO files are the only code that directly interacts with TypeORM / the database.
- Create a DTO file per service; keep DTOs small helpers that orchestrate DAO calls (no business logic).
- Make changes consistent with the style and file naming already used in the repo.
- Be interactive: show plans, show diffs, request confirmation before applying.

Pre-check steps (interactive)
1. List all service files found under src/core/services and show them to me. (Expect: `address.service.ts`, `otp.service.ts`, `permission.service.ts`, `role.service.ts`, `user.service.ts` — verify actual list.)
2. Show current controller files that reference any service or direct DB access. (Example: `src/api/controllers/user.controller.ts`.)
3. Show existing DAO and DTO files (we already have `src/core/dao/user.dao.ts` and `src/core/dto/user.dto.ts` created). Confirm what exists before proceeding.

Refactor plan (for agent to show & confirm before editing)
1. For each service X in src/core/services:
   - Create a DAO file: src/core/dao/{x}.dao.ts (if not exist).
     - DAO must:
       - import appDataSource and the relevant Entity (e.g., UserEntity).
       - create a private repository property: appDataSource.getRepository(Entity).
       - export a class named {X}Dao with CRUD methods (create, findById, findAll, updateById, deleteById, plus any domain-specific finders used in services).
       - export default new {X}Dao();
     - DAO is the ONLY file performing repository.save(), repository.find(), repository.findOneBy(), repository.update(), repository.delete(), repository.findBy(), etc.
   - Create a DTO file: src/core/dto/{x}.dto.ts
     - DTO must:
       - import the {X}Dao default export.
       - export small async functions the services will call (eg. createX, getXById, getAllX, updateX, deleteX, findBySomething).
       - DTO functions should be thin wrappers around DAO class methods and should NOT include business rules (validation/role checks/crypto).
       - Export named functions (not a class) for ease of use in services.
2. Update the service file src/core/services/{x}.service.ts:
   - Remove any direct repository/db operations in the service.
   - Keep business logic in the service (validation, role checks, password hashing, OTP verification, token generation, address update orchestration, sanitization, etc.).
   - For database operations, call the DTO functions you created (src/core/dto/{x}.dto.ts).
   - Ensure all service functions are the single place controllers call; controllers must not call DTO/DAO directly.
   - Add/restore thin CRUD wrapper service methods if controllers expect them (but prefer service methods that compose DTO calls — i.e., controllers should call service.getAllUsers() and that method should call DTO.getAllUser()).
3. Update controllers in src/api/controllers:
   - For each controller method, ensure it calls only service functions (not DTO or DAO) for both CRUD and business operations.
   - If any controller currently calls DTO or DAO directly (e.g., our earlier transient state had controllers calling UserDto), change it so controller calls Service functions instead.
   - Service should sanitize sensitive fields (e.g., remove password) before returning—service or controller may do sanitization but be consistent: prefer service level.
4. Tests and build:
   - After edits for each service, run TypeScript compiler (npx tsc or npm run build) and report errors/warnings to me. Do not modify code to fix compile errors without my confirmation (you may propose fixes in diffs).
   - Where an error is purely stylistic (useless constructor, or linter-like warnings), list them and ask whether to auto-fix.

Implementation details and naming conventions
- DAO filename and symbol: for `user` service use `src/core/dao/user.dao.ts` exporting `class UserDao { ... }` and `export default new UserDao();`
- DTO filename and symbol: for `user` use `src/core/dto/user.dto.ts` exporting functions: `createUser`, `getIndividualUser`, `getAllUser`, `updateUser`, `userDeletion`, `getUserByUsername`, `getUserByEmail`.
- Service file should import DTO functions like: import * as UserDto from "../dto/user.dto";
- Service business functions should be named clearly: e.g., `registerUser`, `performUpdateUser`, `login`, `resetPassword`, and CRUD helpers: `getAllUsers`, `getIndividualUser`, `deleteUser` — controllers call these.
- Error handling: maintain existing pattern (controllers expect service to throw objects with status/message). However, before mass changes, ask me if we should replace `throw { status, message }` with an `HttpError` class. (This is optional but recommended.)
- Keep password hashing in Service (business logic), keep `getEncryptedPassword` or equivalent inside service (not in DTO/DAO).
- DTOs should not import TypeORM, only DAO imports.

Files to create for each service (agent checklist)
- For each service file X found:
  - Create `src/core/dao/{x}.dao.ts` (if not exist)
  - Create `src/core/dto/{x}.dto.ts` (if not exist)
  - Update `src/core/services/{x}.service.ts` to:
    - remove direct db operations
    - use DTO functions for all database ops
    - keep business logic
  - Update controllers that call {x} to only call the service methods (search controller files for direct use of DTO/DAO).
  - Example services: `user`, `role`, `permission`, `address`, `otp`. Confirm actual set before editing.

Safety & interactivity rules (agent MUST follow)
1. Do not run or suggest any git operations.
2. Before modifying any file, show me a short plan listing files to change and a unified diff preview (or the generated patch). Wait for my explicit approval to apply.
3. When you apply changes, report the exact files changed and run TypeScript compile; show compiler output and any remaining warnings.
4. If a change would be large/risky (e.g., changing controller interfaces, renaming exported symbols), explicitly list the breaking changes and ask for confirmation.
5. After completing the full refactor, run `npm run build` (or `npx tsc`) and report success or list compile errors; if errors exist, propose fixes and wait.
6. If any runtime setup (environment keys, local DB) is required to run integration tests, ask me before trying to run anything requiring network or DB access.

Deliverables after each service refactor
- A one-paragraph summary of what you changed and why.
- A list of changed/created files with exact paths.
- The TypeScript build output (success or error listing).
- Any suggestions for follow-up refactors (e.g., introduce `HttpError`, centralize sanitization, unit tests to cover service/DTO/DAO).

Example single-service concrete steps (the agent should show this example and ask for approval)
1. For `user`:
   - Create: `src/core/dao/user.dao.ts` (class `UserDao` with repo methods).
   - Create/update: `src/core/dto/user.dto.ts` (thin wrappers around `UserDao` — you already have one; validate and expand if needed).
   - Update: `src/core/services/user.service.ts`:
     - Move any direct repository usage into DAO.
     - Keep business logic (hashing, OTP, token generation, address updates) inside service.
     - Use DTO functions for CRUD.
   - Update: `src/api/controllers/user.controller.ts`:
     - Ensure it calls only `UserService` methods for all flows.
2. Show the proposed diffs for all changed files, wait for my confirmation, then apply.

Final acceptance criteria
- All controllers call only service methods.
- Services contain business logic and call DTO functions for DB work.
- DTOs call DAO classes; DAOs are the only code using TypeORM repository APIs.
- Project compiles with TypeScript (no runtime DB access required for compile).
- Agent followed the interactive rules above (show plan, await approval, show diffs, compile, report).

Start by listing the services you found and the files you plan to create for each service. Wait for my confirmation before applying any edits.
