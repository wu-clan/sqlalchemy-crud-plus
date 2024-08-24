---

**Documentation**: <a href="https://fastapi-practices.github.io/sqlalchemy-crud-plus" target="_blank">https://fastapi-practices.github.io/sqlalchemy-crud-plus</a>

**Source Code**: <a href="https://github.com/fastapi-practices/sqlalchemy-crud-plus" target="_blank">https://github.com/fastapi-practices/sqlalchemy-crud-plus</a>

---

## Installing

=== "pip"

    ```sh
    pip install sqlalchemy-crud-plus
    ```

=== "pdm"

    ```sh
    pdm add sqlalchemy-crud-plus
    ```

## 示例

=== "api.py"

    ```py
    from typing import Annotated
    
    from fastapi import APIRouter

    router = APIRouter()


    @router.get('/{pk}', summary="获取实例")
    async def get_ins(pk: Annotated[int, Path(...)]) -> InsParam:
        ins = await ins_service.get_ins()
        return InsParam(ins)
    ```

=== "model.py"

    ```py
    from sqlalchemy.orm import declarative_base

    Base = declarative_base()
    
    
    class ModelIns(Base):
        # sqlalchemy model
        pass
    ```

=== "schema.py"

    ```py
    from pydantic import BaseModel

    
    class InsParam(BaseModel):
        # field
        pass
    ```

=== ":star: crud.py"

    ```py
    from sqlalchemy.ext.asyncio import AsyncSession

    from sqlalchemy_crud_plus import CRUDPlus
    

    class CRUDIns(CRUDPlus[ModelIns]):
        async def get(self, db: AsyncSession, pk: int) -> ModelIns:
            return await self.select_model(db, pk)
    
    # singleton
    ins_dao: CRUDIns = CRUDIns(ModelIns)
    ```

=== "service.py"

    ```py
    class InsService:
        async def get_ins():
            async with async_db_session(pk: int) as db:
                ins = ins_dao.get(db, pk)

    ins_service = InsService()
    ```

## 互动

[WeChat / QQ](https://github.com/wu-clan)

## 赞助

如果此项目能够帮助到你，你可以赞助作者一些咖啡豆表示鼓励：[Sponsor](https://wu-clan.github.io/sponsor/)